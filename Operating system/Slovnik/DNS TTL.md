---
aliases: [TTL v DNS]
tags: [slovnik]
---

# DNS TTL

**Time To Live** u [[DNS]] záznamu – kolik sekund si smí resolvery a klienti odpověď pamatovat v cache. Např. TTL 3600 = hodina.

---

## Podrobně

- vysoké TTL = méně dotazů, ale změna adresy se šíří pomalu
- nízké TTL = změny rychle, víc dotazů
- před plánovanou změnou adresy se TTL dočasně sníží
- pozor: jiný význam než [[TTL]] v [[IP adresa|IP]] paketu (počet hopů)

**Souvisí:** [[DNS]], [[03a_DNS_obecne]]
