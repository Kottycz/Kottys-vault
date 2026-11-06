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

**Souvisí:** [[PDU]], [[MTU]], [[MAC adresa]], [[IP adresa]], [[FCS]]
