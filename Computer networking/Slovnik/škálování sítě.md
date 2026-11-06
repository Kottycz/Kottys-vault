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

**Souvisí:** [[modulární zařízení]], [[redundance]], [[schéma IP adresování]], [[topologie]], [[Budovani_male_site]]
