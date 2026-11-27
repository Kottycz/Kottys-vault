---
aliases: [Protocol Data Unit, jednotka dat protokolu]
tags: [slovnik]
---

# PDU

**Protocol Data Unit** – jednotka dat protokolu. Název, který data dostanou na konkrétní vrstvě podle toho, jaká hlavička je zrovna obaluje.

---

## Podrobně

### PDU podle vrstev

| Vrstva ([[OSI]]) | PDU | Co přidává |
| :-- | :-- | :-- |
| Aplikační / Prezentační / Relační | **Data** | samotný obsah |
| Transportní | **Segment** ([[TCP]]) / **Datagram** ([[UDP]]) | [[port\|porty]], poř. čísla |
| Síťová | **Paket** | [[IP adresa\|IP adresy]] |
| Spojová | **Rámec (frame)** | [[MAC adresa\|MAC adresy]], [[FCS]] |
| Fyzická | **Bity** | signál na médiu |

### Jak to souvisí se zapouzdřením

Při odesílání se data postupně balí (viz [[zapouzdření]]) – každá vrstva přidá svoji hlavičku a tím vznikne nová PDU:

```
Odesílání (shora dolů):

Data
└─► [TCP hl.][Data]              = Segment
    └─► [IP hl.][TCP hl.][Data]  = Paket
        └─► [MAC hl.][IP hl.][TCP hl.][Data][FCS] = Rámec
            └─► 01010110101...   = Bity
```

Při příjmu se to naopak postupně rozbaluje (dekapsulace) – každá vrstva sundá svoji hlavičku a předá obsah vrstvě nad sebou.

### Mnemotechnika

**D**ata – **S**egment – **P**aket – **R**ámec – **B**ity

(shora dolů, jak data sestupují k drátu)

### Jak PDU projde sítí

```
PC          switch         router         server
data         —              —             data
segment      —              —             segment
paket        —             paket          paket
rámec       rámec          rámec          rámec
bity        bity           bity           bity
```

- switch pracuje s rámcem, paket uvnitř neotvírá,
- router rámec rozbalí, podívá se do paketu, rozhodne o cestě a zabalí paket do **nového rámce** pro další linku,
- data a segment zůstávají od zdroje k cíli stejné.

### Segment vs. datagram

U [[TCP]] se PDU transportní vrstvy jmenuje **segment**, u [[UDP]] se často říká **datagram**.

**Souvisí:** [[zapouzdření]], [[TCP]], [[UDP]], [[IP adresa]], [[MAC adresa]], [[MTU]], [[OSI]]
