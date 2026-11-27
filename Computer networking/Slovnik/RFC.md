---
aliases: [Request For Comments]
tags: [slovnik]
---

# RFC

**Request For Comments** – dokument popisující internetový standard, protokol nebo postup. Vydává je [[IETF]], každý má své číslo.

---

## Podrobně

### Co to je

Navzdory názvu ("žádost o připomínky") jde o **oficiální dokumentaci** internetových protokolů. Když chceš vědět, jak přesně něco funguje, najdeš to v příslušném RFC.

### Známá RFC

| Číslo | Co popisuje |
| :-- | :-- |
| RFC 791 | [[IPv4]] |
| RFC 793 | [[TCP]] |
| RFC 768 | [[UDP]] |
| RFC 8200 | [[IPv6]] |
| RFC 1918 | privátní IPv4 rozsahy |
| RFC 2131 | [[DHCP]] |
| RFC 4861 | [[NDP]] |

### Vlastnosti

- **Nikdy se nemění** – když se standard aktualizuje, vyjde **nové RFC**, které to staré nahradí (označí se jako "obsoleted by RFC xxxx"). Původní zůstává navždy dostupné.
- **Číslují se postupně** od roku 1969, dnes jich je přes 9000
- Jsou veřejně a zdarma dostupné

### Stavy RFC

Ne každé RFC je platný standard – můžou být ve stavu Proposed Standard, Internet Standard, Informational, Experimental nebo Historic (překonané).

### Aprílová RFC

Tradičně 1. dubna vychází žertovné RFC – např. RFC 1149 "přenos IP paketů poštovními holuby".

### Jak se RFC číst

Na `rfc-editor.org` najdeš každé RFC podle čísla. Klíčová slova **MUST**, **SHOULD**, **MAY** (velkými písmeny) mají přesný význam: MUST = povinné, SHOULD = doporučené, MAY = volitelné (definuje to RFC 2119).

### RFC se nemění

Vydané RFC se už nikdy neupravuje. Když se protokol změní, vyjde **nové RFC** s novým číslem a staré označí jako zastaralé (obsoleted). Např. původní [[TCP]] RFC 793 nahradilo RFC 9293.

**Souvisí:** [[IETF]], [[IEEE]], [[ISO]], [[IANA]]
