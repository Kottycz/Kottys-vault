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

### Kolizní doména

Kolize vznikají jen uvnitř jedné [[kolizní doména|kolizní domény]]. Switch má každý port jako samostatnou kolizní doménu, při full-duplex kolize úplně mizí. Hub má všechny porty v jedné kolizní doméně.

### Kolik kolizí je moc

Na half-duplex lince jsou kolize běžné, ale když jich je víc než pár procent z odeslaných rámců, linka je přetížená. Na full-duplex lince musí být kolizí **nula**.

### Příkaz na vynulování

`clear counters fa0/1` vynuluje počítadla rozhraní. Pak sleduješ, jestli kolize znovu přibývají. Bez vynulování vidíš čísla klidně za několik týdnů.

**Souvisí:** [[late collision]], [[CSMA-CD]], [[half-duplex]], [[full-duplex]], [[runt]], [[duplex]]
