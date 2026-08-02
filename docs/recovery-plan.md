# Recovery plan (validated)

**Device:** Nothing Phone (3a), Nothing OS 3.2, build `Asteroids_V3.2-251013-1406`
**State:** bootloader unlocked, only `fastboot` reachable, screen on "start boot"
**Hazard:** MEDIUM, flashing is reversible. A wipe is permanent, so it is checkpoint-gated.

**Principle:** root-cause first, cheapest step first, and each gate decides by fresh command output, never by assumption.

## Working hypotheses, cheapest first

| # | Hypothesis | Test |
|---|---|---|
| H0 | The OS chain is fine; "start boot" is a one-time bootloader prompt | `fastboot reboot`, watch the boot attempt |
| H1 | A rooting-patched `boot`/`init_boot` aborts early boot | flash stock images over both slots |
| H2 | A Magisk module under `/data/adb/modules` crashes boot | boot to safe mode (VOL-) so no modules load |
| H3 | `/data` is corrupt from the root attempt | `fastboot -w` (last resort, spoken approval required) |

Priority runs H0, then H1, then H2, then H3. Any test that boots to the launcher ends the plan.

## Phase A: prove the link (read-only)

1. `fastboot getvar all` with a hard timeout. A prior `getvar` hang of 120s on a flaky bus was the reason this phase exists. Bounded retry: max 3 replugs within 5 minutes, then stop.
2. Record `current-slot`, `partition-size:boot`, `partition-size:init_boot`, `version-bootloader`, `version-baseband`, `build-number`.
3. Compare partition sizes against the staged images (boot 100663296 B, init_boot 8388608 B) and against the build meta. A mismatch means halt and re-verify the staged images.

**Gate:** `getvar` answers within the limit and the sizes and firmware match Nothing OS 3.2.

## Phase B: test H0 (no writes)

1. `fastboot reboot`.
2. Poll `adb shell getprop sys.boot_completed` with a condition-based loop for up to 5 minutes. `boot_completed=1` means success.
3. If the device returns to the prompt without attempting a boot, it may be a one-time wait for power. Wait 10s, press Power once, and watch again.

**Gate:** the device drops back to `fastboot` only after a real boot attempt. H0 is then false and H1 starts.

## Phase C: test H1 (writes, boot partitions only)

1. `fastboot flash boot_a <staged>/boot.img` and `boot_b` for the same image. Explicit slot names are the correct spelling; `fastboot flash --slot=all` is invalid syntax for `flash`.
2. Try `fastboot flash init_boot_a` and `init_boot_b` only if the bootloader accepts the write. On this device it refuses with a download-size limit, so init_boot stays stock.
3. Verify partition sizes after the flash, before any reboot. Mismatch means stop.
4. `fastboot reboot` and poll `sys.boot_completed`. Success ends the plan.

**Gate:** every flash returns `OKAY`, sizes match after the write, and no other partition was touched. `vbmeta` is never part of this phase.

## Phase D: safe mode, then wipe (checkpointed)

- **Safe mode:** power off, `fastboot reboot`, hold VOL- through boot until the launcher shows "Safe mode". Disable the bad module there, then reboot normally. Data is preserved.
- **Wipe:** `fastboot -w` is the only destructive action and runs only with explicit spoken approval, then a fresh stock boot.

## Phase E: verification (evidence before claims)

1. `getprop ro.build.version.release` returns 15, matching Nothing OS 3.2.
2. `getprop ro.boot.verifiedbootstate` returns `green`.
3. Root is gone: `su -c true` fails and no Magisk bits are left in `/sbin`.
4. The flash-to-launcher transition is captured in the boot log.

## Golden invariants

1. The bootloader stays unlocked until the device is confirmed booted. Never relock early.
2. `vbmeta` is not part of the rescue path. Restoring stock AVB is an optional post-success step.
3. `PWR + VOL-DOWN` re-enters `fastboot` at any point, so every step is crash-safe.
4. One hypothesis at a time, each verified, before the next.

## Done

`fastboot reboot` reaches the launcher and every Phase E check passes.