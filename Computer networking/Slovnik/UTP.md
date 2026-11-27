---
aliases: [Unshielded Twisted Pair, nestíněná kroucená dvojlinka]
tags: [slovnik]
---

# UTP

**Unshielded Twisted Pair** – nestíněná kroucená dvojlinka. Nejběžnější kabel pro Ethernet. Obsahuje 4 páry vodičů zakroucené k sobě, zakončené konektorem RJ-45.

---

## Podrobně

### Proč jsou vodiče zakroucené

Kroucení potlačuje **přeslechy** (crosstalk) mezi páry a rušení zvenčí. Každý pár má jinou délku zákrutu, aby se páry navzájem nerušily. Proto se při zapojování konektoru **nesmí páry rozplétat víc než na ~13 mm**.

### Kategorie

| Kategorie | Rychlost | Frekvence |
| :-- | :-- | :-- |
| Cat 5 | 100 Mb/s | 100 MHz |
| **Cat 5e** | 1 Gb/s | 100 MHz |
| **Cat 6** | 1 Gb/s (10 Gb/s do 55 m) | 250 MHz |
| Cat 6a | 10 Gb/s (100 m) | 500 MHz |
| Cat 7, 8 | 10–40 Gb/s | 600+ MHz |

### Maximální délka

**100 metrů** pro Ethernet (90 m pevný rozvod + 2× 5 m propojovací kabely). Delší úsek = potřeba [[switch]] nebo optika.

### Zapojení konektoru

| Norma | Použití |
| :-- | :-- |
| **T568A** | méně častá |
| **T568B** | v ČR běžnější |

- **Přímý kabel** (straight-through) – oba konce stejně (B–B). Pro spojení různých zařízení (PC ↔ switch).
- **Křížený kabel** (crossover) – konce různě (A–B). Pro spojení stejných zařízení (PC ↔ PC, switch ↔ switch).

Díky [[Auto-MDIX]] to dnes moderní zařízení řeší samo a na typu kabelu nezáleží.

### UTP vs. STP

[[STP kabel]] má navíc stínění proti rušení – používá se v průmyslu nebo blízko silových kabelů. UTP je levnější, ohebnější a pro běžné prostředí dostačuje.

### Kategorie a rychlosti

| Kategorie | Rychlost | Poznámka |
| :-- | :-- | :-- |
| Cat 5e | 1 Gb/s | minimum pro dnešní sítě |
| Cat 6 | 1 Gb/s (10 Gb/s do 55 m) | |
| Cat 6a | 10 Gb/s na 100 m | |
| Cat 8 | 25/40 Gb/s do 30 m | datová centra |

### Postup krimpování konektoru RJ-45

1. odstranit plášť asi 2–3 cm,
2. rozplést páry a srovnat podle T568B (oranžovobílá, oranžová, zelenobílá, modrá, modrobílá, zelená, hnědobílá, hnědá),
3. zarovnat a zkrátit vodiče, ponechat co nejméně rozpletené délky,
4. zasunout do konektoru až na konec (plášť musí být uvnitř konektoru),
5. zakrimpovat kleštěmi a otestovat testerem.

### Chyby při zakončení

Prohozené páry, rozpletené vodiče na dlouhém úseku (zvýšený přeslech), plášť mimo konektor (kabel se vytrhne). Projeví se jako nefunkční linka nebo [[CRC]] chyby.

**Souvisí:** [[STP kabel]], [[Auto-MDIX]], [[NIC]], [[switch]], [[full-duplex]]
