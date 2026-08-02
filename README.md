# Nothing Phone (3a) bootloop recovery

A documented rescue of a Nothing Phone (3a) stuck in a boot loop after a rooting attempt. This repo holds the record: the hypotheses, the commands, the evidence, and the one change that fixed it.

**Result: resolved. The device boots into Android 15. No user data was wiped.**

## Quick summary

- Device: Nothing Phone (3a), Nothing OS 3.2, build `Asteroids_V3.2-251013-1406`
- Symptom: after a root attempt, the phone only answered in `fastboot`. The screen sat on the bootloader's "start boot" prompt
- Root cause: the rooted boot image failed early boot, so the device looped
- Fix: flashed the stock `boot` image to both A/B slots
- Outcome: boot completed, `sys.boot_completed=1`, app data intact

Two findings carry the lesson.

One is platform. The device is Qualcomm, not MediaTek. The AVB fingerprint decodes as `qti/qssi_64/…` and the EFS partitions (`fsc`, `fsg`, `modemst1`) match the Qualcomm layout. A Qualcomm rescue flashes `boot`, `init_boot`, `vendor_boot`, and `vbmeta`. A MediaTek rescue flashes `lk` and `preloader`. Get that wrong and nothing you do will help.

The other is that `init_boot` never had to be flashed. The bootloader rejects a download to it with "Requested download size is more than max allowed". The partition reports `0x800000` (8 MiB) via `getvar`, and `fastboot flash` refuses anything larger. The breakage was the patched `boot` image; restoring stock `boot` to both slots was the whole fix.

## Evidence

Before the restore:

```bash
fastboot devices           # present, device only responds in fastboot
# USB mode 18d1:d00d (fastboot)
```

After the restore:

```bash
adb devices                # <redacted serial>  device
lsusb                      # 18d1:4e11 (Android OS mode)
adb shell getprop ro.build.version.release    # 15
adb shell getprop sys.boot_completed          # 1
fastboot devices           # empty, no longer in fastboot
```

Staged images, each checksum-verified against the build archive:

- `boot.img` → `600cfdca01e779ecf5c27e4c510d711b236c60740df8126b84562672f61fbd05` (100663296 B, 96 MiB)
- `init_boot.img` → `09ed43aedb0efcf62bd3967a36b106840a05eeb3e04b7ebc3d4d5184855dbb19` (8388608 B, 8 MiB, not flashed)

## How it was fixed, step by step

The plan ran cheapest-first, and no step wrote to the phone until cheaper steps had failed with fresh command output.

**Step 1: prove the link (no writes).** `fastboot getvar` answered within the time limit and the partition sizes matched the staged build's sizes. Any mismatch meant stop and re-stage.

**Step 2: test the "start boot" prompt (no writes).** `fastboot reboot` and watch. On this build the "start boot" screen is a one-time wait for power, not a crash loop. When the device did not proceed on its own, one press of Power continued it once the stock boot was in place.

**Step 3: restore stock boot, both slots (writes).** Flashed the stock image, one slot at a time, using explicit slot names:

```bash
fastboot flash boot_a /path/to/stock/boot.img
fastboot flash boot_b /path/to/stock/boot.img
```

Then verified the partition sizes after flashing, before any reboot.

**Step 4: boot and verify.** `fastboot reboot`, poll `sys.boot_completed`, then run the evidence block above. `init_boot` was never flashed; the bootloader rejects the download, so we did not force it.

The full validated plan lives in `docs/recovery-plan.md`, the evidence records in `docs/recovery-completed.md`, and a separate cross-AI review pass (which caught a `fastboot flash --slot=all` syntax error in the original draft) in `docs/cross-ai-review.md`.

## Reproduce

If a Nothing 3/3a (or another AVB+A/B Qualcomm device on Android 13+) is looping after a root attempt:

1. Put the device in `fastboot`. Confirm it is Qualcomm, not MediaTek (look for EFS partitions or the `qti/qssi` AVB fingerprint).
2. Stage stock `boot.img` and `init_boot.img` for the exact build on the device. Check `getvar build-number` first, and verify SHA-256 against your archive.
3. Run the no-write tests first. A "start" screen may be a one-time prompt, not a loop.
4. Flash stock `boot` to both slots with explicit slot names. Do not reinvent `--slot=all`; the correct form is `boot_a` / `boot_b`.
5. Verify partition sizes after the write, then `fastboot reboot`.

This is a record of one specific rescue. Partition names and sizes vary by device; confirm yours before flashing anything.