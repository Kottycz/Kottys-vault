# Postavte si školní IT

> Verze: 2026-10-03

V tomto vaultu postupně vybudujete funkční IT infrastrukturu střední školy na Windows Server 2025 a Windows 11 — a zdokumentujete ji tak, aby ji po vás mohl převzít někdo jiný.

## Než začnete

1. **[[00-pravidla-prace-s-vaultem|Pravidla práce s vaultem]]** — jak vault funguje, kam psát vlastní práci, jak odevzdávat a jak se hodnotí. **Přečtěte jako první.**
2. **[[00-pribeh-skoly|Příběh školy]]** — škola CyberSchool, její obory a lidé, pro které infrastrukturu stavíte.
3. **[[__zadani|Co má být na konci projektu]]** a **[[_vysledek|jak se pozná, že je hotovo]]**.

## Struktura každého modulu

| Soubor | Obsah | Kdy ho dostanete |
|---|---|---|
| `__zadani.md` | Co má být na konci modulu a jak to vypadá | s vydáním modulu |
| `cast0.md` | Teorie k modulu | s vydáním modulu |
| `_vysledek.md` | Jak se pozná, že je modul hotový | s vydáním modulu |
| `cast1.md`, `cast1-powershell.md`, … | Postup správného řešení (GUI a PowerShell) | po kontrole vaší práce |

Vaše vlastní dokumentace patří do složky `Moje dokumentace` — šablony `postup.md` a `overeni.md` dostanete s každým modulem.

## Vydané moduly

| Modul | Zadání | Teorie | Výsledek | Moje dokumentace |
|---|---|---|---|---|
| Modul 0 — Příprava | [[Modul 0 Příprava/__zadani\|zadání]] | [[Modul 0 Příprava/cast0\|teorie]] | [[Modul 0 Příprava/_vysledek\|výsledek]] | [[Moje dokumentace/Modul 0 Příprava/postup\|postup]] · [[Moje dokumentace/Modul 0 Příprava/overeni\|ověření]] |
| Modul 1 — Domain Controller | [[Modul 1 Domain Controller/__zadani\|zadání]] | [[Modul 1 Domain Controller/cast0\|teorie]] | [[Modul 1 Domain Controller/_vysledek\|výsledek]] | [[Moje dokumentace/Modul 1 Domain Controller/postup\|postup]] · [[Moje dokumentace/Modul 1 Domain Controller/overeni\|ověření]] |

Modul 0 se prochází třikrát: pro **SRV1-DC** před Modulem 1, pro **PC1-WIN** před Modulem 2 a pro **SRV2-FS** před Modulem 6.

## Připravujeme

Modul 2 — DHCP · Modul 3 — DNS · Modul 4 — Active Directory · Modul 5 — Group Policy · Modul 6 — File Server a Storage · Modul 7 — File a FTP Services · Modul 8 — Print Services

> Doporučení: po dokončení každého modulu si udělejte snapshot virtuálních strojů — případnou chybu pak opravíte bez stavění všeho znovu.
