# Data, hrozba, riziko

TryHackMe: **FGP-Data,hrozba,riziko**. Základní pojmy: co jsou data a informace, jak je třídit a chránit a jaký je rozdíl mezi **[[hrozba|hrozbou]]**, **[[zranitelnost|zranitelností]]** a **[[riziko|rizikem]]**.

| # | Místnost | Téma |
| :-- | :-- | :-- |
| 1 | Data, hrozba, riziko | data, klasifikace, hrozba × zranitelnost × riziko |
| 2 | [[02_Kyberneticke_hrozby_a_CTI\|Kybernetické hrozby]] | typy hrozeb, [[CTI]], [[OSINT]] nástroje |
| 3 | [[03_Zaklady_zranitelnosti\|Základy zranitelností]] | typy zranitelností, [[CVSS]]/[[VPR]], [[NVD]], [[Exploit-DB]] |

## Úniky dat

- **[[únik dat|Únik dat]] (data breach)** – odcizení nebo zveřejnění dat, týká se milionů uživatelů a je čím dál častější
- jen dva největší úniky 21. století zasáhly zhruba **3,5 miliardy lidí**, nejmenší z top 15 „jen" 134 milionů

### Top 15 největších úniků dat 21. století

| # | Firma | Kdy | Dopad | Pozn. |
| :-- | :-- | :-- | :-- | :-- |
| 1 | **Yahoo** | 2013–2014 | 3 miliardy účtů | útočníci „state-sponsored"; hodnota firmy při prodeji Verizonu klesla o ~350 mil. USD |
| 2 | Sina Weibo | březen 2020 | 538 mil. účtů | čínský Twitter, data prodávána na dark webu za ~1 800 Kč |
| 3 | Marriott | 2014–2018 | 500 mil. zákazníků | útočníci v systému Starwood 4 roky, čísla pasů a karet |
| 4 | Adult Friend Finder | říjen 2016 | 412,2 mil. účtů | 99 % hesel prolomeno kvůli slabému **[[hash\|SHA-1]]** |
| 5 | MySpace | 2013 | 360 mil. účtů | prodáno na dark webu za 6 BTC |
| 6 | NetEase | říjen 2015 | 235 mil. účtů | e-maily a hesla v plaintextu |
| 7 | Zynga | září 2019 | 218 mil. účtů | hacker Gnosticplayers, hesla SHA-1 |
| 8 | LinkedIn | 2012 a 2016 | 165 mil. účtů | hesla SHA-1, prodáno za 5 BTC |
| 9 | Dubsmash | prosinec 2018 | 162 mil. účtů | prodej na Dream Market |
| 10 | Adobe | říjen 2013 | 153 mil. záznamů | hesla a údaje o kartách |
| 11 | MyFitnessPal | únor 2018 | 150 mil. účtů | hesla SHA-1 i bcrypt |
| 12 | Equifax | 29. 7. 2017 | 147,9 mil. zákazníků | **neopravená zranitelnost** webové aplikace, špatná segmentace sítě |
| 13 | eBay | květen 2014 | 145 mil. uživatelů | ukradené přihlašovací údaje 3 zaměstnanců |
| 14 | Canva | květen 2019 | 137 mil. účtů | hesla bcrypt, Gnosticplayers |
| 15 | Heartland Payment Systems | březen 2008 | 134 mil. karet | **[[SQL injection]]**, firma vyřazena z [[PCI DSS]] |

**Poučení:** slabé hashování hesel (SHA-1), neopravené zranitelnosti a ukradené účty zaměstnanců jsou nejčastější příčiny.

## Proč mají data hodnotu

- chráníme víc než hesla: **osobní údaje, finance, obchodní dokumenty, zdravotní záznamy, duševní vlastnictví**
- zneužití → krádež identity, finanční podvody, průmyslová špionáž
- chránit se musí i **metadata** – prozradí zvyky, aktivity a preference uživatelů

## Data a informace

- **Data** – nezpracované prvky (čísla, text, obrázky), samy o sobě nemusí mít význam
- **Informace** – data zasazená do **kontextu**, nesou srozumitelné a užitečné sdělení
- informace = data, která nám **řeknou něco nového**; např. `3+2=5` je pro předškoláka informace, pro středoškoláka už ne

### Klasifikace dat a informací (podle obsahu)

1. **Osobní údaje – [[PII]]** (jméno, adresa, rodné číslo…) – častý cíl krádeže identity a phishingu
2. **Citlivé obchodní informace** – plány, finance, smlouvy → špionáž, vydírání
3. **Duševní vlastnictví** – patenty, autorská práva, obchodní tajemství
4. **Provozní informace** – interní postupy, směrnice → sabotáž
5. **Informace o zaměstnancích** – mzdy, hodnocení, disciplinární záznamy
6. **Zdravotní informace – [[PHI]]** – diagnózy, léčba, předpisy
7. **Vládní informace** – národní bezpečnost, utajované vojenské informace

### Úrovně klasifikace ([[klasifikace dat]])

| Úroveň | Význam |
| :-- | :-- |
| **Veřejné** | zveřejnění nemá žádný dopad |
| **Interní** | jen pro vnitřní použití |
| **Důvěrné** | zveřejnění organizaci poškodí |
| **Vysoce důvěrné** | zveřejnění způsobí značné škody |

- pomáhá plnit předpisy a standardy: **[[GDPR]], [[HIPAA]], PCI DSS, [[NIST]], [[ISO 27001]]**

### Životní cyklus dat

1. **Vytvoření a pořízení** – ruční zadání, senzory, generování, import z jiných systémů
2. **Uložení** – digitálně, na papíře, v hlavě člověka (to jde chránit jen smluvně)
3. **Používání a sdílení** – ochrana přístupu a sdílených dat
4. **Archivace** – retence dat, uchování např. kvůli doložení
5. **Zničení a smazání** – papír skartovat, digitální data trvale smazat **všude** (i zálohy), u prodávaných zařízení smazat nebo zničit médium

Zkráceně: data jsou **uložená**, **přenášená** nebo **používaná** – ve všech stavech je potřeba je chránit.

### Ochrana dat

- **Šifrování** – při přenosu i v klidu
- **Kontrola přístupu** – role, oprávnění, **[[MFA]]**
- **Bezpečnostní monitorování** – audit přístupů, **[[SIEM]]** pro detekci anomálií
- **Zálohování a obnova** – plán obnovy po havárii ([[DRP|Disaster Recovery Plan]])

Strategie: identifikovat a klasifikovat data → **hodnotit rizika** → bezpečnostní politika → školení lidí.

## Význam dat pro rozhodování

- **Strategický nástroj** – analýza trendů, predikce (Big Data, ML, AI)
- **Kvalita dat** – chyby a duplicity vedou ke špatným rozhodnutím (např. chyba v pacientském záznamu)
- **Etika a soukromí** – GDPR, souhlas se zpracováním, transparentnost
- **Inovace** – IoT a senzory, např. prediktivní údržba aut
- **Řízení dat** – **Data Governance**: pravidla, role, odpovědnosti

## Hrozba, zranitelnost, riziko

| Pojem | Definice | Analogie s domem |
| :-- | :-- | :-- |
| **[[hrozba\|Hrozba]]** | potenciální událost nebo aktér, který může zneužít zranitelnost a ohrozit [[cia_triada\|CIA]] (útok, lidská chyba, přírodní katastrofa) | někdo se vloupá a odnese věci |
| **[[zranitelnost\|Zranitelnost]]** | slabina nebo chyba v systému, aplikaci nebo procesu (chyba v SW, špatná konfigurace, návrh) | rozbitý zámek, otevřené okno |
| **[[riziko\|Riziko]]** | pravděpodobnost, že hrozba zneužije zranitelnost, a jak velká bude škoda | čtvrť s vysokou kriminalitou, chybí alarm |

- **riziko = pravděpodobnost × dopad**
- příklad: nemocniční databáze má známou zranitelnost a vyšel na ni **[[exploit]]** → hrozba je reálná, je třeba zhodnotit riziko a naplánovat opravu

## Otázky z místnosti

| Otázka | Odpověď |
| :-- | :-- |
| Jste doktor a načítáte data pacienta. K jakým datům přistupujete? | **Zdravotní informace** |

## Související

- [[Principy kybernetické bezpečnosti]] – CIA triáda
- [[02_Kyberneticke_hrozby_a_CTI]], [[03_Zaklady_zranitelnosti]]
