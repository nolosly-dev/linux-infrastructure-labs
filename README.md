# Linux Infrastructure & Systems Engineering Labs

Operational runbooks, incident reports, and system administration drills executed in a bare-metal Fedora environment targeting Enterprise Linux (RHEL/Fedora Server).

## 👤 Operator Profile

* **Operator:** Abdulrahman Mahmoud
* **Focus:** Linux Systems Administration & Infrastructure Engineering
* **Current Operations:** Pursuing a B.Sc. while maintaining hands-on Linux administration labs, system troubleshooting, and Bash automation workflows.
* **Target Environment:** Red Hat Enterprise Linux (RHEL), Fedora Server, POSIX-compliant UNIX environments.

---

## 🛠️ Bare-Metal Host & Lab Environment Architecture

All incident drills and service configurations are executed inside isolated, headless QEMU/KVM virtual machines hosted on a bare-metal Fedora workstation.

### Workstation Hardware & OS
* **Host Model:** HP EliteBook 745 G6 (AMD Ryzen 7 PRO 3700U, 16GB RAM)
* **Host OS:** Fedora Linux 44 (KDE Plasma Desktop Edition x86_64)
* **Kernel:** `Linux 7.2.10-200.fc44.x86_64`
* **Root Filesystem:** Btrfs on NVMe (`/dev/dm-0`, 951GB) with subvolume snapshot management
* **Terminal Environment:** Konsole / Bash 5.3 + `tmux` session persistence

### Hypervisor Stack & Guest Topology
* **Hypervisor:** Headless QEMU/KVM (`qemu-system-x86_64`) with KVM hardware acceleration enabled (`-enable-kvm`)
* **Guest Target:** Fedora Server / RHEL 9 (`fedora_lab.qcow2`)
* **Storage Allocation:** Copy-on-Write (CoW) virtual disks (`disk1.qcow2`, `disk2.qcow2`) for LVM and storage triage
* **Snapshot Management:** Native `qemu-img` snapshot trees for instant recovery prior to griefing payloads

```bash
# Hypervisor Execution Command
qemu-system-x86_64 -enable-kvm -nographic -smp 4 -m 2048 \
  -hda fedora_lab.qcow2 \
  -hdb disk1.qcow2 \
  -hdc disk2.qcow2
```

## 📂 Laboratory Domain Index

This repository is structured into domain-specific modules. Each directory contains a dedicated index, architectural notes, and step-by-step incident resolution runbooks.

  

|**Domain Module**|**Core Competencies**|**Directory Link**|
|---|---|---|
|**00: Infrastructure & Git**|Headless QEMU/KVM architecture, local SSH keys, Git workflows, snapshot state recovery.|[`./00-infrastructure-and-git`](https://www.google.com/search?q=./00-infrastructure-and-git/)|
|**01: Users & Permissions**|POSIX ownership (`chmod`/`chown`), extended POSIX ACLs (`getfacl`/`setfacl`), special bits (SGID, Sticky), `sudoers` privileges.|[`./01-users-and-permissions`](https://www.google.com/search?q=./01-users-and-permissions/)|
|**02: Process & System Control**|`systemd` unit files, service recovery, process signal handling (`kill`/`pkill`), `journalctl` triage, resource monitoring.|[`./02-process-and-system-control`](https://www.google.com/search?q=./02-process-and-system-control/)|
|**03: Storage & Filesystems**|Disk partitioning (`fstab`), mount management, LVM volume expansion, filesystem integrity, disk space alerts.|[`./03-storage-and-filesystems`](https://www.google.com/search?q=./03-storage-and-filesystems/)|
|**04: Networking & Services**|Socket state inspection (`ss`), interface management (`ip`), DNS resolution (`dig`/`nslookup`), SSH configuration.|[`./04-networking-and-services`](https://www.google.com/search?q=./04-networking-and-services/)|
|**05: Firewalls & Security**|`firewalld` rule management, port bindings, service exposure, base SELinux state triage.|[`./05-firewalls-and-security`](https://www.google.com/search?q=./05-firewalls-and-security/)|

## 📜 Runbook Methodology

Incident write-ups inside each module follow an enterprise First Contact Resolution (FCR) workflow:

  

$$\text{Read \& Parse} \longrightarrow \text{Audit System} \longrightarrow \text{Isolate Fix} \longrightarrow \text{Verify as User}$$

Every report contains:

  

1. **Ticket Metadata & Context:** Priority, affected user roles, and raw user complaint.
    
      
    
2. **Griefing Payload:** The exact bash execution script used to break the guest system.
    
      
    
3. **Live Triage Log:** Unedited terminal history and observations during problem isolation.
    
      
    
4. **Resolution & Verification:** Remediation commands and multi-role access checks (`su - <user> -c`).
