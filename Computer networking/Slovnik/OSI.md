---
aliases: [OSI model, ISO/OSI, referenční model OSI]
tags: [slovnik]
---

# OSI

**Open Systems Interconnection** – referenční model síťové komunikace o **7 vrstvách**. Vydala ho organizace [[ISO]] jako normu ISO/IEC 7498 – proto se mu říká i **ISO/OSI**.

---

## Podrobně

### Sedm vrstev

| #   | Vrstva      | Co dělá                                   | [[PDU]] |
| :-- | :---------- | :---------------------------------------- | :------ |
| 7   | Aplikační   | rozhraní pro aplikace ([[HTTP]], [[DNS]]) | Data    |
| 6   | Prezentační | formát, komprese, šifrování               | Data    |
| 5   | Relační     | navazuje a udržuje relace                 | Data    |
| 4   | Transportní | [[TCP]]/[[UDP]], číslo [[port\|porty]]    | Segment |
| 3   | Síťová      | [[IP adresa\|IP adresy]], směrování       | Paket   |
| 2   | Spojová     | [[MAC adresa\|MAC adresy]], rámce         | Rámec   |
| 1   | Fyzická     | signál na médiu                           | Bity    |

### Mnemotechnika (shora dolů)

**A**plikační – **P**rezentační – **R**elační – **T**ransportní – **S**íťová – **S**pojová – **F**yzická

### OSI vs. TCP/IP model

| OSI (7) | TCP/IP (4) |
| :-- | :-- |
| Aplikační + Prezentační + Relační | **Application** |
| Transportní | **Transport** |
| Síťová | **Internet** |
| Spojová + Fyzická | **Network Access** |

### Rozdíl mezi modely

- **OSI** – teoretický, výrobcem nezávislý model. Vznikl "od stolu" jako norma, slouží hlavně k popisu a výuce.
- **TCP/IP** – praktický model odvozený od protokolů, které se reálně používají. Vznikl dřív než OSI.

V praxi se mluví oběma – např. "vrstva 3" (podle OSI), ale používají se protokoly z TCP/IP.

**Souvisí:** [[ISO]], [[IEEE]], [[IETF]], [[PDU]], [[zapouzdření]]
