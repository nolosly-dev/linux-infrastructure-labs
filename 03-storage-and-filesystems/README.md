# Module 03: storage-and-filesystems

Core system administration drills focusing on disk management, block capacity troubleshooting, inode exhaustion triage, LVM volume manipulation, and `fstab` mount points.

## 📋 Incident Runbook Ledger

| Ticket ID / Topic | Severity | Core Domain Focus | Status | Runbook Link |
| :--- | :--- | :--- | :--- | :--- |
| **Storage & Inode Triage** | HIGH | Disk Space (`df -h`), Inode Exhaustion (`df -i`), `du` Sorting, Find One-Liners | ✅ Documented | [storage-and-inode-exhaustion-triage.md](./storage-and-inode-exhaustion-triage.md) |

## 🛠️ Module Objectives
* Isolate storage bloat versus descriptor (inode) exhaustion under tight terminal constraints.
* Master native disk auditing toolchains (`df`, `du`, `sort`, `uniq`, `find`) without third-party dependencies.
* Build muscle memory for emergency root filesystem recovery and partition triage.
