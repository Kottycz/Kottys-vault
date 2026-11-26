---
aliases: [DNS forwarder, conditional forwarder, root hints]
tags: [slovnik]
---

# forwarder

[[DNS]] server, kterému náš [[DNS]] **předá dotaz**, na který sám nezná odpověď. Např. SRV1-DC předá `www.skola.cz` veřejnému resolveru.

---

## Podrobně

- klient tak potřebuje **jediný [[DNS]]** (řadič) – vyřeší školní i internetová jména
- **conditional forwarder** – jen pro vybranou doménu (partnerská firma)
- bez forwarderu použije server **root hints** (kořenové servery)
- [[DNS]] Manager → vlastnosti serveru → **Forwarders**

**Souvisí:** [[DNS]], [[03b_DNS_na_radici]]
