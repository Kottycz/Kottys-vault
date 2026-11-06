---
aliases: [-f, -ff, --mtu, fragmentace IP]
tags: [slovnik]
---

# Fragmentace paketů (`-f`)

Rozdělení IP dat na **menší fragmenty**, aby se ztížila detekce [[firewall|firewallem]] a [[IDS]].

*Příklad: `sudo nmap -sS -p80 -f MACHINE_IP`.*

---

## Podrobně

- `-f` = fragmenty po **8 bajtech**, `-ff` = po **16**
- `--mtu` – vlastní velikost (násobek 8)
- `--data-length NUM` – připojí náhodná data
- skládá se podle [[IP ID]] a ofsetu v [[hlavička IP|hlavičce IP]]

**Souvisí:** [[IDS]], [[firewall]], [[hlavička IP]], [[IP ID]], [[nmap]]
