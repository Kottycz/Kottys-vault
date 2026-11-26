---
aliases: [ověřovací protokol AD]
tags: [slovnik]
---

# Kerberos

Protokol, kterým se v doméně **ověřují uživatelé** (port 88). Po přihlášení dostaneš od řadiče „vstupenku“ (ticket) a heslo už se po síti znovu neposílá.

---

## Podrobně

- používá **časová razítka** → rozdíl hodin max **5 minut**, jinak odmítne i správné heslo
- ochrana proti **replay útoku**
- proto čas v doméně řídí [[FSMO|PDC]] emulator ([[FSMO]]) a synchronizace přes [[NTP]]

**Souvisí:** [[AD DS]], [[UTC]], [[00c_Cas_jazyk_soukromi]]
