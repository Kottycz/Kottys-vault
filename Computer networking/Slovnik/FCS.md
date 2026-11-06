---
aliases: [Frame Check Sequence, kontrolní součet rámce]
tags: [slovnik]
---

# FCS

**Frame Check Sequence** – 4bajtové pole na **konci** ethernetového rámce. Slouží ke kontrole, jestli se rámec cestou nepoškodil.

---

## Podrobně

### Jak funguje

```
Odesílatel:
  spočítá CRC ze všech polí rámce  →  zapíše ho do FCS

Příjemce:
  spočítá CRC znovu ze stejných polí
  ├─ shoduje se s FCS  →  rámec je v pořádku, zpracuje se
  └─ neshoduje se      →  rámec je poškozený, ZAHODÍ se
```

Používá se algoritmus **CRC-32** (cyklický redundantní součet).

### Důležité: jen detekce, ne oprava

FCS umí poškození **pouze poznat**, ne opravit. Vadný rámec se prostě zahodí a spojová vrstva o tom nikoho neinformuje. O nápravu se musí postarat vyšší vrstva – typicky [[TCP]], který si chybějící data vyžádá znovu. U [[UDP]] se data prostě ztratí.

### Umístění v rámci

```
[Preambule][Cíl MAC][Zdroj MAC][Typ][   Data   ][FCS]
   8 B        6 B       6 B      2 B  46–1500 B   4 B
```

FCS je jediné pole **za** daty – proto se mu říká také "trailer" (patička), na rozdíl od hlavičky.

### Kdy rámce padají

Vysoký počet FCS chyb na portu obvykle znamená:

- vadný nebo příliš dlouhý kabel
- rušení (blízko silových vedení)
- špatně zalisovaný konektor
- **duplex mismatch** (viz [[half-duplex]])
- vadný port nebo [[NIC]]

Zobrazení na Cisco: `show interfaces` → řádek s CRC errors.

**Souvisí:** [[NIC]], [[switch]], [[zapouzdření]], [[PDU]], [[MAC adresa]]
