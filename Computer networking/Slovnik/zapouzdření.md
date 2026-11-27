---
aliases: [encapsulation, enkapsulace, dekapsulace]
tags: [slovnik]
---

# zapouzdření

**Proces, při kterém každá vrstva přidá k datům svoji hlavičku**, než je předá vrstvě pod sebou. Opačný proces při příjmu se nazývá **dekapsulace**.

---

## Podrobně

### Princip

Data putují modelem shora dolů a postupně se obalují – jako když dáváš dopis do obálky, obálku do krabice a krabici na paletu:

```
ODESÍLÁNÍ (zapouzdření)          PŘÍJEM (dekapsulace)

Aplikační:  Data                        Data
              ↓ + TCP hlavička            ↑ − TCP hlavička
Transportní: [TCP][Data]               [TCP][Data]
              ↓ + IP hlavička             ↑ − IP hlavička
Síťová:      [IP][TCP][Data]           [IP][TCP][Data]
              ↓ + MAC hlavička + FCS     ↑ − MAC hlavička
Spojová:     [MAC][IP][TCP][Data][FCS] [MAC][IP][TCP][Data][FCS]
              ↓                          ↑
Fyzická:     101101010...              101101010...
```

Každá vrstva "vidí" jen svou hlavičku – obsah nad ní je pro ni jen data.

### Co která hlavička přidává

| Vrstva | Přidává | Aby se vědělo |
| :-- | :-- | :-- |
| Transportní | [[port\|porty]], poř. čísla | která **aplikace** |
| Síťová | [[IP adresa\|IP adresy]] | který **počítač / síť** |
| Spojová | [[MAC adresa\|MAC adresy]], [[FCS]] | které **zařízení v LAN** + kontrola chyb |

### Související pojmy

- **Segmentace** – rozdělení velkých dat na menší části (limituje [[MTU]])
- **Multiplexování** – víc datových toků po jednom kanálu zároveň
- **Sekvencování** – očíslování částí, aby šly složit ve správném pořadí

### Co se děje na routeru

[[router|Router]] rámec **dekapsuluje** na paket, rozhodne kam dál, a zabalí ho do **nového rámce** s jinými MAC adresami. IP adresy se přitom nemění – proto MAC adresy platí jen pro jeden úsek cesty, IP pro celou.

### Příklad: otevření webové stránky

```
Data:    GET /index.html
Segment: [TCP hlavička: zdroj. port 50123, cíl. port 80] + data
Paket:   [IP hlavička: 192.168.1.5 → 203.0.113.10] + segment
Rámec:   [Ethernet: MAC PC → MAC brány] + paket + [FCS]
Bity:    1010110…
```

Cílová MAC je MAC **brány**, ne serveru – server je v jiné síti.

### Na switchi vs. na routeru

- **switch** – rozbalí jen rámec (vrstva 2), podívá se na MAC a pošle rámec dál beze změny,
- **router** – rozbalí rámec až na paket (vrstva 3), sníží TTL, podle IP rozhodne a zabalí paket do **nového rámce** s novými MAC adresami.

### Ve Wiresharku

V detailu paketu vidíš zapouzdření přesně: Frame → Ethernet II → Internet Protocol → Transmission Control Protocol → Hypertext Transfer Protocol.

**Souvisí:** [[PDU]], [[MTU]], [[MAC adresa]], [[IP adresa]], [[FCS]]
