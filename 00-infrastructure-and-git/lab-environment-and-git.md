# Lab 00: Headless QEMU/KVM Infrastructure & Git Version Control

## 1. Architectural Overview
Before provisioning enterprise services or executing system troubleshooting, a reliable, remote-accessible lab infrastructure and version-controlled documentation workflow must be established.

### Host & Remote Access Stack
* **Remote Terminal Transport:** Mobile phone (Termux) connects to the host machine via **Tailscale Mesh VPN** over encrypted SSH.
* **Session Persistence:** Managed using `tmux` sessions (`tmux a -t vm`) allowing continuous VM state management during network transitions or remote operation.
* **Hypervisor Layer:** Headless **QEMU/KVM** execution bypassing resource-heavy desktop virtualizers.

```bash
# Example Headless VM Launch Command
qemu-system-x86_64 -enable-kvm -nographic -smp 4 -m 2048 \
  -hda fedora_lab.qcow2 \
  -hdb disk1.qcow2 \
  -hdc disk2.qcow2
```
