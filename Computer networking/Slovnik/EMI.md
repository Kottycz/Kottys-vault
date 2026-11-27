---
aliases: [elektromagnetické rušení, RFI, rádiofrekvenční rušení, přeslech, crosstalk]
tags: [slovnik]
---

# EMI

**Elektromagnetické rušení** (Electromagnetic Interference) – vnější elektromagnetické pole, které narušuje signál v kabelu. Příbuzné je **RFI** (rádiofrekvenční rušení) a **přeslech**.

---

## Podrobně

### Tři druhy rušení

| Typ | Zdroj |
| :-- | :-- |
| **EMI** | motory, zářivky, silové kabely, výtahy |
| **RFI** | rádiové vysílače, Wi-Fi, mobilní sítě |
| **Přeslech (crosstalk)** | sousední pár vodičů **ve stejném kabelu** |

### Jak se rušení brání

- **Kroucení vodičů** – páry v [[UTP]] jsou zakroucené, rušení zasáhne oba vodiče stejně a vzájemně se vyruší. Každý pár má jinou délku zákrutu, aby se páry nerušily navzájem.
- **Stínění** – [[STP kabel]] má kovovou fólii nebo oplet, který rušení odvádí (musí být uzemněný)
- **Optika** – [[optické vlákno]] je vůči EMI i RFI **úplně imunní**, protože přenáší světlo, ne elektřinu
- **Dodržení vzdálenosti** od silových kabelů

### Projevy v síti

Rušený kabel se pozná podle:

- vysokého počtu **[[CRC]] / [[FCS]] chyb** na portu
- kolísavého [[throughput|výkonu]]
- opakovaných výpadků linky
- nižší dosažené rychlosti, než jakou kabel podporuje

### Chyby při instalaci

- Rozpletení párů v konektoru víc než ~13 mm
- Příliš ostré ohyby kabelu
- Vedení souběžně se silovým kabelem na dlouhém úseku
- Použití nestíněného kabelu v průmyslovém prostředí

### Přeslech (crosstalk)

Zvláštní druh rušení, kdy signál z jednoho páru vodičů v kabelu ruší sousední pár. Nejčastější je na koncích kabelu, kde jsou páry rozpletené (**NEXT**, Near-End Crosstalk). Proto se při zakončování kabelu nemají páry rozplétat víc, než je nutné.

### Jak to poznat

Rušení se projeví jako [[CRC]] chyby a ztracené rámce v `show interfaces`. Typicky se objeví jen v určitou dobu (když běží stroj, výtah, klimatizace).

### Které médium je odolné

| Médium | Odolnost |
| :-- | :-- |
| [[UTP]] | nízká, chrání jen kroucení párů |
| [[STP kabel]] | vyšší, stínění |
| [[optické vlákno]] | úplná, přenáší světlo, ne elektřinu |

**Souvisí:** [[UTP]], [[STP kabel]], [[optické vlákno]], [[FCS]], [[CRC]]
