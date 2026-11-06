---
aliases: [collision, collisions]
tags: [slovnik]
---

# kolize

**Kolize** – dvě zařízení začnou vysílat na sdíleném médiu **ve stejnou chvíli** a signály se zničí; rámce se pak musí poslat znovu. Příklad: dva počítače na hubu vyšlou současně → kolize → oba čekají náhodnou dobu a zkusí to znovu.

---

## Podrobně

### Kde jsou normální

- v [[half-duplex]] (huby, staré sítě) ano, řeší je [[CSMA-CD]],
- na [[full-duplex]] lince se **nikdy nesmí objevit**.

### V `show interfaces`

- **collisions** – počet znovu odeslaných zpráv kvůli kolizi,
- [[late collision]] – kolize po 512 bitech rámce, vždy chyba.

### Co s nimi

Zkontrolovat [[duplex]] na obou koncích (nesoulad je nejčastější příčina), kabel a jeho délku.

**Souvisí:** [[late collision]], [[CSMA-CD]], [[half-duplex]], [[full-duplex]], [[runt]], [[duplex]]
