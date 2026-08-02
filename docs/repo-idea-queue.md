# Repo Idea Queue

Trending-first backlog. Each idea should answer exactly one narrow question. Star the ones that are hot now, deprioritize the ones that are cold.

## Selection criteria
- One repo = one narrow question. No multi-tool mega-repos.
- Trend-aligned (search volume, recent issues, hot takes, vendor activity).
- Authored response to a real problem I hit, used, or reverse engineered.
- Ship-ready in one focused session (research → data → README → CI → release).

## Status legend
- `Backlog` - queued, no work started
- `Researching` - web/code research underway
- `Drafting` - README/CI/docs being written
- `Shipped` - pushed, topics set, release tagged, star history badge live

## Star/profile-boost signals (rank-ordered)
1. Search demand for exact problem phrase (e.g. "Nothing Phone 3a bootloop")
2. Recent filing as a public issue/Reddit thread with 100+ upvotes
3. No dominant existing repo for the exact question (low competition, high intent)
4. Topic exists as a GitHub topic tag with >1k repos (joins a real neighborhood)
5. Vendor recently shipped/broke something (window of relevance)

---

## Active idea queue

### Tier 1 - Trending, high intent, ship next

| Status | Repo name | One-line question | Trend signal | Topic neighborhood |
| - | - | - | - | - |
| Shipped | `nothing-phone-bootloop-recovery` | How do I rescue a Nothing Phone (3a) bootloop with no data loss? | Failed OTA wave on Nothing OS 3.2 build `Asteroids_V3.2-251013-1406`; threads spike weekly | `nothing-phone`, `fastboot`, `bootloop`, `android-recovery` |
| Backlog | `nothing-phone-3a-safe-root` | What is the current safest root path on Nothing OS 3.2 that survives OTA? | XDA/Lemmy root threads re-spike on every Nothing OS point release | `magisk`, `kernelsu`, `apkpatcher-2022`, `root`, `nothing-phone` |
| Backlog | `no-data-ota-rescue-cheatsheet` | What is the universal no-data-loss OTA-fail rescue cheatsheet for Qualcomm A/B devices? | Qualcomm A/B OTA fail class is the most-bumped category on Android Reddit every cycle | `android`, `ota`, `qualcomm`, `ab-partitions`, `data-recovery` |
| Backlog | `fastboot-snippets` | A single curated `fastboot` snippet file: every command I actually used during rescues | `fastboot` has 18k+ monthly searches and no canonical snippet repo exists | `fastboot` (GitHub topic, 1k+), `adb`, `android-tools`, `cheatsheet` |
| Backlog | `kernelsu-nothing-3a` | What is the verified KernelSU install path on Nothing Phone (3a) on Nothing OS 3.2? | KernelSU "next" releases break compat with Nothing kernels weekly | `kernelsu`, `nothing-phone`, `kernel`, `root` |

### Tier 2 - Trendy, ship if time permits

| Status | Repo name | One-line question | Trend signal | Topic neighborhood |
| - | - | - | - | - |
| Backlog | `nvidia-driver-rollback` | How do I roll back to a known-good NVIDIA driver on Linux after a bad upgrade? | Linux driver regressions trend every release; rollback procedures are scattered | `nvidia`, `linux`, `kernel`, `gpu`, `rollback` |
| Backlog | `pipewire-latency-fix` | How do I fix PipeWire crackling on a fresh Ubuntu install without dropping to PulseAudio? | PipeWire regressions trend every cycle | `pipewire`, `linux-audio`, `ubuntu`, `pulseaudio` |
| Backlog | `rclone-backup-3-2-1` | A copy-paste `rclone` config that implements 3-2-1-1-0 backup for $5/mo | `rclone` topic has 2k+ repos; no canonical 3-2-1 config exists | `rclone`, `backup`, `3-2-1`, `borg`, `restic` |
| Backlog | `linux-laptops-framework-13` | Framework Laptop 13 Linux gotchas: what breaks every kernel bump and how to fix it fast | Framework owners are vocal and the kernel compat matrix changes monthly | `framework-laptop`, `linux`, `kernel`, `hardware` |
| Backlog | `home-assistant-backup-restore` | How do I back up and restore Home Assistant OS without losing ZHA/Zigbee pairings? | HA backups regress at least once per major release | `home-assistant`, `home-automation`, `backup`, `zigbee`, `zha` |

### Tier 3 - Cool, lower urgency

| Status | Repo name | One-line question | Trend signal | Topic neighborhood |
| - | - | - | - | - |
| Backlog | `openwrt-vlan-cheatsheet` | A copy-paste VLAN config for OpenWrt that works for ISP + guest + IoT isolation | OpenWrt 23+ VLAN DSL changes break old guides monthly | `openwrt`, `vlan`, `networking`, `router` |
| Backlog | `esp32-ota-rollback` | How do I implement ESP32 OTA rollback that actually survives a botched update? | ESP-IDF v5.x OTA rollback docs are sparse and Stack Overflow traffic is rising | `esp32`, `esp-idf`, `ota`, `firmware`, `rollback` |
| Backlog | `proxmox-vm-backup-cheatsheet` | A copy-paste Proxmox backup script with retention policy and offsite mirror | Proxmox 8 backup prowler hit every cycle | `proxmox`, `backup`, `vm`, `lxc` |
| Backlog | `git-history-rewrite-safe` | A safe-by-default recipe for rewriting public Git history without breaking forks | BFG and git-filter-repo guides age poorly | `git`, `bfg`, `git-filter-repo`, `history-rewrite` |

---

## Done log

| Date | Repo | Outcome |
| - | - | - |
| 2026-08-03 | `nothing-phone-bootloop-recovery` | Shipped with hero image, badges, CI, social preview, OG image, 12 topics, v1.0.0 release |

---

## How to ship the next one
1. Confirm the trend signal above is still live (re-run the search, check the thread).
2. `searchcode.code_search` for prior art on the question (avoid reinventing).
3. `context7` for any library docs you'll cite in the README.
4. `composio` `web_search` for the most recent issue/Reddit thread timestamp.
5. Copy `templates/README.template.md` as the starting README.
6. Author facts into `docs/recovery-plan.md` first; the README cites it.
7. Run `avoid-ai-writing` in detect mode; require 0 em dashes / 0 curly quotes / 0 AI-isms.
8. Run `design-taste-frontend` for hero, badges, callouts, tables, changelog, star history.
9. Re-run anti-slop check; ship if 0/0/0.
10. Push, then via Composio set 8-12 topic tags, set homepage, create v1.0.0 release with anti-slop checked notes.
11. Update this queue: move row from Tier to Done log.