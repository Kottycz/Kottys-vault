---
aliases: [služba Netlogon]
tags: [slovnik]
---

# Netlogon

Služba na řadiči domény, která mimo jiné **zapisuje do [[DNS]]** záznam A řadiče a **[[SRV záznam|SRV]] záznamy**, podle kterých ho klienti najdou.

---

## Podrobně

- záznamy ve složkách `_msdcs`, `_sites`, `_tcp`, `_udp` zóny
- obnovení registrace: `nltest /dsregdns`
- zajišťuje i ověřování přihlášení a secure channel počítačů

**Souvisí:** [[SRV záznam]], [[03b_DNS_na_radici]]
