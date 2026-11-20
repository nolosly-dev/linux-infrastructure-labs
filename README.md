# Linux Infrastructure Labs

Break-and-fix scenarios on a headless Fedora VM (QEMU/KVM), documented as incident write-ups: symptoms, triage, root cause, fix, verification and prevention.

These are simulations in a personal lab, not production incidents.

## Environment

- Host: Fedora 45 (KDE), 15 GB RAM
- Guest: Fedora Server VM, 4 vCPU, 2 GB RAM, three extra virtual disks
- Boot script: [environment/vm.sh](environment/vm.sh)

## Labs

| # | Lab | Skills | Status |
|---|-----|--------|--------|
| 01 | [Storage and inode usage triage](labs/01-storage-and-inode-triage.md) | df, du, dd, find | Published |
| 02 | Broken fstab and locked-root recovery | fstab, rescue mode | In progress |
