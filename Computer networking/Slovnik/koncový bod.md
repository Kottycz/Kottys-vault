---
aliases: [endpoint, hostitel, host]
tags: [slovnik]
---

# koncový bod

**Endpoint (hostitel)** – individuální počítačový systém nebo zařízení, které funguje jako síťový klient. Mezi běžné koncové body patří notebooky, stolní počítače, servery, chytré telefony a tablety.

---

## Podrobně

### Proč je zabezpečení náročné

Zabezpečení koncových zařízení je jedním z nejnáročnějších úkolů správce sítě, protože zahrnuje **lidskou povahu** – i sebelepší technické zabezpečení selže, když zaměstnanec klikne na phishingový odkaz nebo použije slabé heslo.

### Co pomáhá

- dobře zdokumentované bezpečnostní zásady
- proškolení zaměstnanců v řádném používání sítě
- antivirové/antimalwarové programy s aktuálními definicemi
- pravidelné aktualizace operačního systému a aplikací

### Typy koncových bodů

- počítače a notebooky,
- mobilní telefony a tablety (často BYOD – vlastní zařízení zaměstnanců),
- tiskárny, IP telefony, IP kamery,
- IoT zařízení (senzory, chytré spotřebiče), často s minimálním zabezpečením.

### Ochrana koncových bodů

| Opatření | K čemu |
| :-- | :-- |
| antivirus / antimalware | najde a odstraní škodlivý software |
| osobní [[firewall]] | filtruje provoz přímo na zařízení |
| aktualizace | záplaty známých zranitelností |
| šifrování disku | ochrana dat při krádeži |
| 802.1X / NAC | do sítě pustí jen ověřená a zabezpečená zařízení |

### Koncový bod vs. zprostředkující zařízení

Koncový bod (host) je **zdroj nebo cíl** komunikace. Zprostředkující zařízení ([[switch]], [[router]], [[AP]], firewall) data jen přenáší.

**Souvisí:** [[malware]], [[firewall]], [[AAA]]
