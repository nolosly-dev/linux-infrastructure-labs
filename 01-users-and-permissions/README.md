# Module 01: Users & Permissions

Core system administration drills focusing on POSIX ownership, special permissions (SUID, SGID, Sticky Bit), extended POSIX ACLs, and `sudoers` least-privilege configurations.

## 📋 Incident Runbook Ledger

| Ticket ID | Severity | Core Domain Focus | Status | Runbook Link |
| :--- | :--- | :--- | :--- | :--- |
| **TICKET #4092** | HIGH | POSIX Ownership, SGID Inheritance, Parent Traversal, Extended ACLs (`setfacl`) | ✅ Resolved | [ticket-01-web-app-permissions.md](./ticket-01-web-app-permissions.md) |

## 🛠️ Module Objectives
* Master directory traversal mechanics and inode execute (`x`) permissions.
* Enforce automated group-based collaboration using the SGID bit (`g+s`).
* Implement surgical multi-team security boundaries using POSIX Extended ACLs.
