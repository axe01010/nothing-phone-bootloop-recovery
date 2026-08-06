# 📱 Nothing Phone Bootloop Rescue

<p align="center">
  <img src="https://img.shields.io/badge/Nothing-Phone-black?style=for-the-badge&logo=nothing&logoColor=white" />
  <img src="https://img.shields.io/badge/Android-3DDC84?style=for-the-badge&logo=android&logoColor=white" />
  <img src="https://img.shields.io/badge/Fastboot-00A651?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Recovery-4285F4?style=for-the-badge" />
</p>

> Documented rescue of a **Nothing Phone (3a)** from a hard bootloop — and a reusable recovery toolkit for Nothing devices.

## 🎯 What Happened

A Nothing Phone (3a) got stuck in a bootloop after a failed OTA update. The device wouldn't boot, wouldn't enter recovery, and was unresponsive to normal button combos. This repo documents the full rescue process and provides reusable tools.

## 🔧 Recovery Process

### Step 1: Diagnose the Bootloop
- Device powers on → shows Nothing logo → restarts → repeat
- Cannot access recovery (Vol Down + Power)
- Cannot access bootloader (Vol Up + Power)
- ADB not detected in bootloop state

### Step 2: Force EDL Mode
- Hold **Vol Up + Vol Down + Power** for 15 seconds
- Screen stays black but device is in EDL (Emergency Download) mode
- Detects as `QHSUSB__BULK` on PC

### Step 3: Flash Stock Firmware
```bash
# Using MSM Download Tool (Windows) or edl (Linux)
# Download official Nothing firmware from Nothing support
edl wipe partitions
edl flash firmware.img
```

### Step 4: Reboot & Verify
```bash
edl reboot
# Device boots normally
```

## 🛠️ Tools & Scripts

| Script | Purpose |
|--------|---------|
| `scripts/detect.sh` | Detects device state (bootloop/EDL/normal) |
| `scripts/flash.sh` | Automated firmware flashing |
| `scripts/backup.sh` | Backup partitions before flashing |
| `scripts/verify.sh` | Post-flash verification |

## 📋 Compatibility

- Nothing Phone (1) ✅
- Nothing Phone (2) ✅
- Nothing Phone (2a) ✅
- Nothing Phone (3a) ✅ (tested)
- Nothing CMF Phone 1 ✅

## ⚠️ Warnings

- Flashing can void warranty
- Always backup before flashing
- Use correct firmware for your exact model
- Bricked devices may need Nothing support

## 📁 Repository Structure

```
nothing-phone-bootloop-recovery/
├── firmware/            # Firmware links & checksums
├── scripts/             # Recovery scripts
├── docs/
│   ├── NOTHING-1.md
│   ├── NOTHING-2.md
│   ├── NOTHING-2A.md
│   ├── NOTHING-3A.md
│   └── CMF-1.md
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

## 🤝 Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Contributions welcome:
- Device-specific recovery guides
- New scripts for detection/flashing
- Firmware checksums & links
- Translations

## 📜 License

MIT License - see [LICENSE](LICENSE)

---

<p align="center">
  Rescued with ❤️ by <a href="https://github.com/axe01010">axe git</a> · Nothing Phone survivor
</p>
