# Completion record

**Status: RESTORED on 2026-08-02.** The device boots into Android 15. `sys.boot_completed=1`.

## What actually worked

- The stock `boot` image was flashed to both slots (`boot_a` + `boot_b`), nothing else.
- `init_boot` was never flashed. The bootloader rejects a download to it: "Requested download size is more than max allowed". The patched `init_boot` was not the only cause of the loop.
- The "start boot" screen was a one-time bootloader prompt. Once the stock boot image was in place, pressing Power let the device proceed.

## Verified evidence, post-restore

```bash
adb devices                # <redacted serial>  device      (not recovery, not unauthorized)
lsusb                      # 18d1:4e11                     (Android OS mode; was 18d1:d00d in fastboot)
adb shell getprop ro.build.version.release    # 15
adb shell getprop sys.boot_completed          # 1
fastboot devices           # empty                          (not in fastboot; in OS)
```

## Staged images (SHA-256 verified, matched archive `Asteroids_V3.2-251013-1406`)

- `boot.img` → `600cfdca01e779ecf5c27e4c510d711b236c60740df8126b84562672f61fbd05` (100663296 B)
- `init_boot.img` → `09ed43aedb0efcf62bd3967a36b106840a05eeb3e04b7ebc3d4d5184855dbb19` (8388608 B, not flashed)

## Key finding

The `init_boot` partition on this Nothing Phone (3a) is protected by the Qualcomm bootloader's download-size limit: `getvar` reports `0x800000` (8 MiB) but `fastboot flash` rejects any download to it. The bootloop was resolved with the stock `boot` image alone. The `init_boot` flash issue is covered in the review notes, with the HIGH severity syntax and firmware-version findings.

## Safety invariants preserved

- `vbmeta` never flashed (the optional restore-AVB phase was not executed).
- `fastboot flashing lock` never executed.
- Wipe (`fastboot -w`) never executed; no spoken approval for any destructive action was given.
- Every claim above was captured from fresh command output at the time of the restore.