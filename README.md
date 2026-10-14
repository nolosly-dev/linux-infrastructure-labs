# 🐧 Linux Infrastructure & Systems Engineering Labs

Welcome! I’m **Abdulrahman Mahmoud**, a Sysadmin & Infrastructure enthusiast operating on **Fedora Linux / RHEL enterprise environments**.

This repository serves as my hands-on technical portfolio—documenting production-style lab scenarios, core system administration, storage management, CLI diagnostic workflows, and real-world troubleshooting drills.

> **Methodology:** My learning workflow pairs AI-driven technical deep dives (Gemini, GPT, Claude) with hands-on CLI experimentation, official documentation, and scenario-based labs to build permanent terminal muscle memory.

---

## 🛠️ Infrastructure & Host Environment

* **Host Hardware:** HP EliteBook 745 G6 (AMD Ryzen 7 PRO 3700U, 16GB RAM, Btrfs)
* **Host OS:** Fedora Linux 44 (KDE Plasma Desktop Edition)
* **Hypervisor Stack:** Raw Headless QEMU / KVM (`qemu-system-x86_64`) with Copy-on-Write (`.qcow2`) snapshots
* **Remote Management:** Tailscale Mesh VPN + SSH + `tmux` session persistence (via Termux)
* **Target Guest OS:** Fedora Server / Red Hat Enterprise Linux (RHEL 9)

---

## 📂 Laboratory Audit Index

| Module | Core Topics | Status |
| :--- | :--- | :--- |
| **`00-infrastructure-and-git`** | Headless QEMU/KVM architecture, Tailscale mesh VPN, SSH keys, Git workflow | ✅ Completed |
| **`01-shell-and-permissions`** | Shell Redirection (`tee`), POSIX ACLs, SUID/SGID, `sudoers` privileges | 🔄 Active |
| **`02-storage-and-lvm`** | `fstab` recovery, LVM volume groups, disk expansion, Swap management | ⏳ Pending |
| **`03-systemd-and-services`** | Custom unit files, `journalctl` audits, service overrides, socket activation | ⏳ Pending |
