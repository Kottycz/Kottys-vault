---
aliases: [hypervisor, Hyper-V]
tags: [slovnik]
---

# hypervizor

Software, který dělí hardware hostitele ([[CPU]], [[RAM]], disky, síť) mezi **[[VM|virtuální stroje]]** a izoluje je od sebe. Např. Hyper-V, VMware ESXi, Proxmox.

---

## Podrobně

- **typ 1 (bare-metal)** – přímo na HW → servery (Hyper-V, ESXi, Proxmox, KVM)
- **typ 2 (hostovaný)** – aplikace v [[operační systém|OS]] → výuka (VirtualBox, VMware Workstation)
- spadne hostitel → spadnou všechny [[VM]] → clustery

**Souvisí:** [[VM]], [[snapshot]], [[00a_Virtualizace_edice_aktivace]]
