# Nothing Phone (3a) bootloop recovery

A documented rescue of a Nothing Phone (3a) stuck in a boot loop after a rooting attempt. This repo holds the record: the hypotheses, the commands, the evidence, and the one change that fixed it.

**Result: resolved. The device boots into Android 15. No user data was wiped.**

## Quick summary

- Device: Nothing Phone (3a), Nothing OS 3.2, build `Asteroids_V3.2-601013-1406`
- Symptom: after a root attempt, the phone only answered in `adb`/`fastboot`.
- Root cause: a bad boot image put the device in a boot loop.
- Fix: flashed the stock `boot` image back.

## Evidence

```bash
adb devices
adb shell getprop ro.build.version.release
adb shell getprop sys.boot_completed
```

## What worked

The full record: [recovery-plan.md](docs/recovery-plan.md), [recovery-completed.md](docs/recovery-completed.md), [cross-ai-review.md](docs/cross-ai-review.md).