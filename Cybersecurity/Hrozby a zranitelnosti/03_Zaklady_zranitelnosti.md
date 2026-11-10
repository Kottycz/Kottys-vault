# Základy zranitelností

TryHackMe: **FGP-Základy zranitelností**. Co je **[[zranitelnost]]**, jaké jsou typy, jak se hodnotí (**[[CVSS]]**, **[[VPR]]**) a kde je hledat (**[[NVD]]**, **[[Exploit-DB]]**).

## Penetrační testy

[[penetrační test|Penetrační test]] = řízený útok na vlastní systém se svolením.

- **Externí testy** – útok zvenku (přes internet)
- **Interní testy** – zevnitř sítě: [[firewall]], [[UTM]], Wi-Fi, web, aplikace, mobilní aplikace, pracovní stanice, mobilní zařízení, zaměstnanci, uživatelé, hesla, informační systémy

## Co je zranitelnost

**Zranitelnost** = slabina nebo chyba v **návrhu, implementaci nebo chování** systému či aplikace. Útočník ji zneužije k přístupu k informacím nebo k neoprávněným akcím.

- **[[NIST]]:** „slabost v informačním systému, postupech, vnitřních kontrolách nebo implementaci, kterou může zneužít zdroj hrozby"
- **NIST Cybersecurity Framework** – cyklus 5 funkcí: **Identifikovat → Chránit → Zjistit → Reagovat → Zotavit se**

### 5 kategorií zranitelností

| Kategorie | Popis | Příklad |
| :-- | :-- | :-- |
| **Operační systém** | chyby v OS, často vedou k **eskalaci oprávnění** | uživatel → správce |
| **(Mis)konfigurace** | špatně nastavená aplikace nebo služba | web ukazuje údaje zákazníků |
| **Slabé / výchozí přihlašovací údaje** | výchozí jméno a heslo | `admin` / `admin` |
| **Aplikační logika** | špatně navržená aplikace | obejití přihlášení přes cookies |
| **Lidský faktor** | zneužití lidského chování | [[phishing]] |

## Hodnocení zranitelností

- **Řízení zranitelností** = hodnocení, kategorizace a náprava zranitelností
- opravit všechno nejde a je to plýtvání – zneužije se jen asi **2 %** zranitelností
- proto se zranitelnosti **bodují** a řeší se nejdřív ty nejnebezpečnější

### CVSS (Common Vulnerability Scoring System)

- od roku **2005**, aktuálně **CVSSv3.1** (v4.0 se chystá), **zdarma a otevřený**, doporučuje ho NIST
- skóre podle: jak snadno se dá zneužít, jestli existuje exploit, jak zasahuje do **[[cia_triada|CIA]]**
- počítá se kalkulačkou z těchto metrik:

| Metrika | Možnosti |
| :-- | :-- |
| **Vektor útoku** | síťový, sousední, lokální, fyzický |
| **Složitost útoku** | nízká, vysoká |
| **Požadovaná oprávnění** | žádná, nízká, vysoká |
| **Interakce uživatele** | žádná, vyžadovaná |
| **Rozsah** | změněný, nezměněný |
| **Důvěrnost / Integrita / Dostupnost** | vysoká, nízká, žádná |

Nejhorší kombinace: síťový útok, nízká složitost, žádná oprávnění, žádná interakce, vysoký dopad na CIA.

| Hodnocení | Skóre |
| :-- | :-- |
| None | 0 |
| Low | 0,1 – 3,9 |
| Medium | 4,0 – 6,9 |
| High | 7,0 – 8,9 |
| Critical | 9,0 – 10,0 |

- ✅ dlouho zavedený, populární, zdarma
- ❌ neurčuje **prioritu**, jen závažnost; přeceňuje dostupnost exploitu (exploit má jen ~20 % zranitelností); skóre se po vyhodnocení skoro nemění

### VPR (Vulnerability Priority Rating)

- moderní rámec firmy **Tenable**, **řízený rizikem** – jak velké [[riziko]] je to **pro danou organizaci**
- když organizace zranitelný software nepoužívá, riziko se nepočítá
- **dynamický** – skóre se mění skoro denně
- jak vzniká: **1.** načtení dat (threat intel, exploit kity, data Tenable, NVD) → **2.** příprava funkcí → **3.** model hrozeb se **strojovým učením** → **4.** skóre hrozby → **5.** kombinace s CVSS (je-li k dispozici) → **6.** výsledné VPR (např. 9,6)
- stupnice jako CVSS, ale **bez kategorie None** (Low 0,0–3,9 … Critical 9,0–10,0)
- ✅ přes 150 faktorů, pomáhá s prioritou oprav
- ❌ není open source, jen s komerční platformou, CIA řeší méně

**Shrnutí:** zdarma a open source → **CVSS**, podle rizika pro firmu → **VPR**.

## Databáze zranitelností

| Pojem | Význam |
| :-- | :-- |
| **Zranitelnost** | slabina v systému nebo aplikaci |
| **[[exploit\|Exploit]]** | akce nebo kód, který zranitelnost zneužije |
| **[[PoC]] (Proof of Concept)** | ukázka, že exploit funguje |

### NVD (National Vulnerability Database)

- seznam všech veřejně kategorizovaných zranitelností – **[[CVE]]** (Common Vulnerabilities and Exposures)
- formát **CVE-ROK-ČÍSLO**, např. **CVE-2017-0144** (zneužil ji **WannaCry**)
- filtry podle kategorie a měsíce; na hledání pro konkrétní aplikaci se moc nehodí

### Exploit-DB

- exploity podle **názvu, autora a verze** softwaru – pro pentestera užitečnější
- obsahuje **PoC** kód, autor: **OffSec**

## Postup při hledání zranitelnosti

1. **[[Version Disclosure]]** – aplikace prozradí název a verzi (např. **Apache Tomcat 9.0.17**)
2. hledat verzi v **Exploit-DB** → pro Tomcat 9.0.17 vyšlo **5 exploitů**
3. vybrat exploit a použít ho

Zranitelnosti se často **kombinují** – malá (zjištění verze) vede k velké (exploit).

**Ukázka ACKme:** junior pentester sleduje seniora → zjistí verzi aplikace → najde exploit → získá přístup a **flag**. Testovat se smí jen IP v rozsahu zakázky (*scope*), nic jiného.

## Otázky z místnosti

| Otázka | Odpověď |
| :-- | :-- |
| Účet z „uživatele" na „správce" – typ zranitelnosti | **Operační systém** |
| Obejití přihlášení přes cookies | **Aplikační logika** |
| Rok první verze CVSS | **2005** |
| Rámec podle rizika pro organizaci | **VPR** |
| Rámec zdarma a open source | **CVSS** |
| Počet CVE v NVD za červenec 2021 | **1554** |
| Autor Exploit-DB | **OffSec** |
| Typ zranitelnosti k zjištění názvu a verze | **Version Disclosure** |
| Flag z ukázky ACKme | **THM{ACKME_ENGAGEMENT}** |

## Související

- [[01_Data_hrozba_riziko]], [[02_Kyberneticke_hrozby_a_CTI]]
- [[Nmap příkazy]] – detekce verzí služeb (`-sV`)
