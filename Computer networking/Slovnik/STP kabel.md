---
aliases: [Shielded Twisted Pair, stíněná kroucená dvojlinka]
tags: [slovnik]
---

# STP kabel

**Shielded Twisted Pair** – stíněná kroucená dvojlinka. Jako [[UTP]], ale navíc má kovové stínění proti elektromagnetickému rušení.

---

## Podrobně

### Typy stínění

| Značení | Stínění |
| :-- | :-- |
| **U/UTP** | žádné (= klasický UTP) |
| **F/UTP** | fólie kolem celého svazku |
| **S/FTP** | opletení kolem svazku + fólie kolem každého páru |
| **U/FTP** | fólie kolem každého páru |

### Kdy použít

- Průmyslové prostředí (motory, svářečky, frekvenční měniče)
- Vedení souběžně se silovými kabely
- Serverovny s vysokou hustotou kabeláže
- Vysokorychlostní přenosy (10 Gb/s a výš)

### Nevýhody

- **Dražší** než UTP
- **Tužší a hůř se ohýbá** – horší manipulace v rozvaděči
- **Musí být uzemněné** – stínění je potřeba svést na zem na obou stranách. Špatně uzemněné stínění funguje jako **anténa** a rušení naopak zhorší.
- Vyžaduje stíněné konektory a stíněné zásuvky (jinak je celá investice zbytečná)

### Pozor na zkratku

STP má v sítích **dva úplně různé významy**:

- **STP kabel** = Shielded Twisted Pair (kabel)
- **STP protokol** = Spanning Tree Protocol (brání smyčkám na [[switch|switchích]], viz [[broadcast]] storm)

Který je který, se pozná z kontextu.

### Uzemnění

Stínění chrání jen tehdy, když je **správně uzemněné** na obou koncích (přes stíněné konektory a uzemněný patch panel). Neuzemněné stínění může fungovat jako anténa a rušení ještě zhoršit.

### Značení typů

| Značení | Význam |
| :-- | :-- |
| U/UTP | bez stínění |
| F/UTP | celkové stínění fólií, páry nestíněné |
| U/FTP | každý pár stíněný fólií |
| S/FTP | celkové stínění opletem + každý pár fólií |

První část = stínění celého kabelu, druhá = stínění párů (F = fólie, S = oplet, U = žádné).

### Kdy vybrat STP

Výroba s motory a svářečkami, vedení vedle silových kabelů, rychlosti 10 Gb/s a víc na delší vzdálenosti (Cat 6a/7 bývají stíněné).

**Souvisí:** [[UTP]], [[switch]], [[NIC]]
