# Kybernetické hrozby a CTI

TryHackMe: **FGP-Kybernetické hrozby**. Co je **[[hrozba|kybernetická hrozba]]**, jak se hrozby třídí, co je **[[CTI]]** a **[[OSINT]]** a jak se pracuje s nástroji **[[urlscan.io]]**, **[[abuse.ch]]** a **[[PhishTool]]**.

## Kybernetické hrozby

**Kybernetická hrozba** = potenciální událost nebo akce, která může **zneužít zranitelnost** k útoku na systémy a data. Zdroj: kyberzločinci, malware, vnitřní hrozby, přírodní katastrofy.

### Základní rozdělení

- **Pasivní** – útočník jen **sleduje** komunikaci, nemění ji
- **Aktivní** – útočník přenášená data **mění** (např. částku v platbě)
- **[[APT]] (pokročilá trvalá hrozba)** – dlouhodobá, vytrvalá infiltrace sofistikovanými technikami

### Skupiny hrozeb

- **Únik informace** – důvěrná data se dostanou k neoprávněným
- **Narušení integrity** – podvržená nebo změněná data
- **Potlačení služby** – uživatelé se nedostanou ke službě (**DoS**)
- **Nelegitimní použití** – neoprávněné využívání zdrojů (např. placených služeb)

### Klasifikace hrozeb

- **Podle zdroje**
  - způsobené **člověkem** – **úmyslné** (smazání, krádež dat) nebo **z nedbalosti** (omylem smazaná data)
  - **vyšší moc** – přírodní katastrofa, požár, výpadek proudu
  - **technické chyby** – selhání HW, chyby SW
- **Podle působení** – **vnitřní** (zaměstnanci) × **vnější** (hackeři, konkurence, organizovaný zločin)
- **Podle cíle**
  - útoky na **[[cia_triada|CIA triádu]]** – důvěrnost (krádež dat), integrita (změna dat), dostupnost (DDoS)
  - útoky na **lidi** (sociální inženýrství, phishing), **technologie** (HW, sítě, SW), **procesy**
- seznam hrozeb je i v **příloze č. 3 vyhlášky o kybernetické bezpečnosti**

### 8 hlavních hrozeb podle ENISA

1. **Ransomware** – zašifruje data a chce výkupné
2. **Malware** – škodlivý software
3. **Sociální inženýrství** – zneužití lidské chyby
4. **Hrozby proti datům** – únik a zveřejnění dat
5. **DoS** – odepření služby
6. **Internetové hrozby** – narušení dostupnosti internetu jako celku
7. **Dezinformace a misinformace**
8. **Útoky na dodavatelský řetězec** – přes dodavatele do cílové organizace

## Threat Intelligence (CTI)

**[[CTI]] (Cyber Threat Intelligence)** = informace **podložené důkazy** o současných i možných hrozbách. Pomáhají hrozbám porozumět, předcházet jim, odhalit je a reagovat. Příklad: **Cisco Talos Intelligence Group**.

Základní otázky: **Kdo útočí? Proč? Co umí? Na jaké stopy ([[IOC]]) si dát pozor?**

### Klíčové aspekty CTI

- **Shromažďování dat** – veřejné zdroje, uzavřené databáze, darknet fóra, honeypoty
- **Analýza hrozeb** – chování útočníků, jejich **[[TTP]]** (taktiky, techniky, postupy)
- **Kontextualizace** – povaha hrozby, dopad, pravděpodobnost, obrana
- **Informování rozhodování** – podklady pro vedení a IT
- **Prevence a reakce** – řešit zranitelnosti dřív, než způsobí škodu

### Typy CTI

| Typ | Pro koho / co |
| :-- | :-- |
| **Strategická** | vedení – trendy a vzory |
| **Taktická** | TTP útočníků, posílení bezpečnostních kontrol |
| **Operační** | konkrétní kampaně, motivace a záměry útočníků |
| **Technická** | konkrétní indikátory – **IP adresy, URL, hashe** |

**Výhody:** proaktivní bezpečnost, lepší detekce, **rychlá reakce**, ochrana před budoucími hrozbami.

## OSINT

**[[OSINT]] (Open Source Intelligence)** = sběr informací z **veřejně a legálně** dostupných zdrojů (weby, sociální sítě, registry, fóra, noviny, články).

- žádné hackování ani nelegální získávání dat
- využití: firmy (reputace, konkurence), státy a policie (zločin, terorismus), bezpečáci (zranitelnosti, útočníci)
- pro CTI je OSINT hlavní zdroj

## Nástroje

### urlscan.io

**[[urlscan.io]]** – bezplatné skenování a analýza webu. Po zadání URL zaznamená domény, IP adresy, načtené zdroje, snímek stránky a použité technologie.

| Záložka | Co ukazuje |
| :-- | :-- |
| **Summary** | IP, registrace domény, historie, snímek |
| **HTTP** | HTTP spojení a stažená data |
| **Redirects** | přesměrování |
| **Links** | odkazy z hlavní stránky |
| **Behaviour** | proměnné a cookies (prozradí framework) |
| **Indicators** | IP, domény a hashe spojené s webem (nemusí být škodlivé) |

### abuse.ch

**[[abuse.ch]]** – projekt Bernské univerzity (Švýcarsko) na sledování **malwaru** a **[[botnet|botnetů]]**.

| Platforma | K čemu |
| :-- | :-- |
| **MalwareBazaar** | databáze vzorků malwaru, upload a lov (YARA, ClamAV, tagy) |
| **FeodoTracker** | **[[C2]] servery** botnetů (Dridex, Emotet, TrickBot, QakBot) |
| **SSL Blacklist** | škodlivé SSL certifikáty a **JA3 otisky** C2 komunikace |
| **URLhaus** | URL, které šíří malware |
| **ThreatFox** | sdílení a export **[[IOC]]** (MISP, Suricata, JSON, CSV) |

### PhishTool

**[[PhishTool]]** – analýza **[[phishing|phishingových]]** e-mailů (verze Community a Enterprise).

- **Headers** – odesílatel, příjemce, IP, časy
- **Received Lines** – cesta e-mailu přes SMTP servery (= počet **skoků**)
- **X-headers** – rozšířené hlavičky
- **Security** – **[[SPF]]**, **[[DKIM]]**, **[[DMARC]]**
- **Attachments**, **Message URLs** – přílohy a odkazy k prověření
- **Resolve** – klasifikace e-mailu a závěr analýzy

**Jak analyzovat .eml bez PhishToolu:** otevřít v Thunderbirdu nebo textovém editoru, případně v terminálu:

```bash
grep -iE "^(from|to):" Email1.eml      # odesílatel a příjemce
grep -ic "^received:" Email1.eml       # počet Received = počet skoků
```

## Otázky z místnosti

| Otázka | Odpověď |
| :-- | :-- |
| Co je Cisco Talos Intelligence Group? | **CTI** |
| Typ CTI s detaily jako IP adresy | **Technická** |
| Výhoda CTI – kontext pro rychlou reakci | **Rychlá reakce** |
| Aspekt CTI – analýza dat z různých zdrojů | **Shromažďování dat** |
| Cisco Umbrella rank TryHackMe (urlscan) | **345612** |
| Počet domén (urlscan) | **13** |
| Registrátor domény | **NAMECHEAP INC** |
| Hlavní IP TryHackMe | **2606:4700:10::ac43:1b0a** |
| Alias malwaru u IOC 212.192.246.30:5555 (ThreatFox) | **Katana** |
| Malware s JA3 51c64c77e60f3980eea90869b68c58a8 | **Dridex** |
| Síť s ASN AS14061 (URLhaus) | **DIGITALOCEAN-ASN** |
| Země IP 178.134.47.166 (FeodoTracker) | **Georgia** |
| Email1 – za koho se útočník vydává | **LinkedIn** |
| Email1 – odesílatel | **darkabutla@sc500.whpservers.com** |
| Email1 – příjemce | **cabbagecare@hotsmail.com** |
| Email1 – počet skoků | **4** |
| Email2 – příjemce | **chris.lyons@supercarcenterdetroit.com** |
| Email3 – název přílohy | **Sales_Receipt 5606.xls** |
| Email3 – malware v příloze | **Dridex** |

## Související

- [[01_Data_hrozba_riziko]], [[03_Zaklady_zranitelnosti]]
- [[Wireshark souhrn]] – analýza provozu
