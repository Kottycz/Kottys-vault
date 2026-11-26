---
aliases: [DNS suffix, connection-specific DNS suffix]
tags: [slovnik]
---

# DNS přípona

Doména, kterou klient automaticky přidá ke krátkému jménu. Např. `srv2-fs` → `srv2-fs.kotrba.cyberschool.internal`.

---

## Podrobně

- klient ji dostane při připojení do domény a z [[DHCP]] (option **015**)
- proto funguje `ping srv2-fs` bez celého jména
- v `ipconfig /all` jako *Connection-specific [[DNS]] Suffix*
- nslookup ji přidává i tam, kde nechceš → píšu **tečku na konci** jména

**Souvisí:** [[FQDN]], [[DHCP scope]], [[01c_Jmeno_domeny_a_DNS]]
