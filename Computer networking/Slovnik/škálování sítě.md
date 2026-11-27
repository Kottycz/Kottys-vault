---
aliases: [škálování, škálovatelnost, scalability]
tags: [slovnik]
---

# škálování sítě

**Postupné zvětšování sítě spolu s růstem firmy** – tak, aby se síť nemusela celá předělávat.

---

## Podrobně

### Proč je potřeba

Malá síť dnes bude za rok možná dvakrát větší – víc zaměstnanců, víc zařízení, víc provozu. Když se na to nepočítá už při návrhu, musí se později vyměňovat i zařízení, která ještě fungují. Proto se už při stavbě sítě volí [[modulární zařízení]] a rychlejší porty než je zrovna potřeba.

### Co je k tomu zapotřebí

| Prvek | Co obsahuje |
| :-- | :-- |
| **Dokumentace sítě** | fyzická a logická topologie, schémata, nastavení zařízení |
| **Inventář zařízení** | seznam zařízení, která v síti jsou nebo ji tvoří |
| **Rozpočet** | kolik se může do sítě investovat (včetně plánovaného nákupu techniky) |
| **Analýza provozu** | jaké protokoly, aplikace a služby síť využívají a kolik provozu potřebují |

Podle analýzy provozu se pozná, **kde** je síť přetížená a kam je potřeba investovat.

### Škálování v praxi

- zařízení s volnými porty nebo sloty
- plánované [[schéma IP adresování|schéma adres]] s rezervou
- [[redundance]], aby růst nezvyšoval riziko výpadku ([[single point of failure]])

### Hierarchický model

Síť se staví ve vrstvách, aby se dala rozšiřovat:

| Vrstva | Úkol |
| :-- | :-- |
| **přístupová** (access) | připojení uživatelů, [[VLAN]], [[PoE]] |
| **distribuční** | směrování mezi VLAN, filtrace, redundance |
| **jádro** (core) | co nejrychlejší přenos mezi částmi sítě |

Přidání nové budovy = nový přístupový switch připojený k distribuci, zbytek sítě se nemění. Menší sítě používají **collapsed core** (distribuce a jádro v jednom).

### Na co myslet při návrhu

- adresní plán s rezervou ([[VLSM]], dost velké podsítě),
- [[modulární zařízení]] nebo stohovatelné switche v jádru,
- směrovací protokol, který zvládne růst ([[OSPF]] s oblastmi),
- dokumentace, aby se v rostoucí síti dalo vyznat.

**Souvisí:** [[modulární zařízení]], [[redundance]], [[schéma IP adresování]], [[topologie]], [[Budovani_male_site]]
