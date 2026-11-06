# Principy kybernetické bezpečnosti

Neexistuje 100% bezpečné řešení – cílem je ztížit útočníkovi přístup, ne dosáhnout dokonalosti. Nejdřív je potřeba znát protivníka (proti čemu/komu chráníme), teprve pak volit odpovídající opatření.

**Data** - informace které už znám 
**Informace** - to co už znám

## CIA triáda

- **Confidentiality (důvěrnost)** – k datům má přístup jen oprávněná osoba
- **Integrity (integrita(neporušenost))** – data nelze neoprávněně změnit, případná změna je detekovatelná
- **Availability (dostupnost)** – systém/služba je dostupná, když je potřeba

Viz [[cia_triada|CIA triáda]]. Důraz na jednotlivé složky se liší podle situace (u nemocničních záznamů je klíčová integrita, u online obchodu důvěrnost karty).

### Jak funguje důvěrnost

- **Šifrování** – data čitelná jen s dešifrovacím klíčem
- **Kontrola přístupu** – kdo smí vidět/používat jaké zdroje
- **Autentizace a autorizace** – ověření identity před přístupem (heslo, biometrika)
- příklady: zdravotnictví (ochrana záznamů pacientů), finanční sektor (údaje o účtech), firmy (obchodní tajemství)
- v bezpečnostních politikách: **klasifikace dat** (kategorie podle citlivosti) a **zásada minimálního oprávnění**

**[[tlp|TLP (Traffic Light Protocol)]]** – schéma značení citlivosti informací a pravidel jejich sdílení, čtyři úrovně:
- **TLP:RED** – jen pro přímo určené osoby, nikam dál
- **TLP:AMBER** – vlastní organizace + klienti, jen pokud nutné k obraně
- **TLP:GREEN** – širší komunita, ne veřejnost
- **TLP:WHITE** – veřejné, bez omezení

### Jak funguje integrita

- **Kontrolní součty a hashovací funkce** – ověří, že soubor nebyl změněn
- **Digitální podpisy** – ověří původ a neporušenost dat
- **Správa oprávnění a auditní záznamy** – kdo, kdy a proč data změnil
- v bezpečnostních politikách: zásady pro manipulaci s daty, pravidelné audity a monitorování, zálohování a obnova
- příklady: databáze (sledovatelnost změn), finanční transakce, integrita zdrojového kódu

### Jak funguje dostupnost

- **Redundance a failover** – duplicitní komponenty přebírají funkci při selhání
- **Zálohování a obnova dat** – Disaster Recovery Plan
- **Údržba a testování** systémů
- v bezpečnostních politikách: plánování kapacity, rychlá reakce na incidenty, ochrana proti útokům typu **DoS/DDoS** (odmítnutí služby)
- příklady: webové služby, zdravotní systémy, bankovnictví

### Rozšíření CIA

- **[[autenticita|Autenticita]] (Authenticity)** – data/soubor skutečně pocházejí z tvrzeného zdroje; podporuje důvěrnost (jen oprávnění mají přístup) i integritu (ověří, kdo dělal změny). Zajišťuje se hesly, biometrikou, tokeny, digitálními certifikáty.
- **[[nepopiratelnost|Nepopiratelnost]] (Non-repudiation)** – zdroj nemůže popřít, že data/objednávku vytvořil on; posiluje integritu (sledovatelnost akcí). Nejčastěji zajištěna **digitálním podpisem** (kryptografie veřejného klíče).

### [[parkerian_hexad|Parkerian Hexad]] (Donn Parker, 1998)

Šest prvků bezpečnosti: Availability, Utility, Integrity, Authenticity, Confidentiality, Possession.

- **Utility (užitečnost)** – i dostupná data jsou k ničemu, pokud nejsou v použitelné formě (např. ztracený dešifrovací klíč)
- **Possession (vlastnictví)** – ochrana dat před neoprávněným odebráním i bez porušení důvěrnosti (např. ukradený zálohovací disk)

## [[dad_triada|DAD triáda]] (opak CIA)

- **Disclosure (zveřejnění)** – opak důvěrnosti
- **Alteration (pozměnění)** – opak integrity
- **Destruction/Denial (zničení/odepření)** – opak dostupnosti

Extrémní ochrana důvěrnosti a integrity může omezit dostupnost, a naopak – bezpečnostní zásady musí tyto tři vyvažovat.

## Tři pilíře kybernetické bezpečnosti

- **Lidé** – nejčastěji nejslabší článek, potřebují školení
- **Technologie** – firewally, IDS/IPS, šifrování, antivir
- **Procesy** – řízení rizik, správa přístupových práv, zálohování, reakce na incidenty

## Životní cyklus kybernetické bezpečnosti

1. **Prevence** – bezpečnostní politiky, školení, firewally, šifrování
2. **Detekce** – SIEM, monitoring, detekce malwaru a anomálií
3. **Reakce** – izolace napadených systémů, odstranění hrozby, obnova provozu, poučení z incidentu

## Bezpečnostní modely

### [[bell_lapadula|Bell-LaPadula]] (důvěrnost)

- **Simple Security Property** – "no read up": nelze číst nad svou úroveň
- **Star (\*) Security Property** – "no write down": nelze zapisovat pod svou úroveň
- **Discretionary Security Property** – přístupová matice (kdo/co smí číst/zapisovat)
- shrnutí: **write up, read down**
- omezení: nezvládá sdílení souborů

### [[biba|Biba]] (integrita)

- **Simple Integrity Property** – "no read down"
- **Star Integrity Property** – "no write up"
- shrnutí: **read up, write down** (opak Bell-LaPadula)
- omezení: nezvládá vnitřní hrozby (insider threats)

### [[clark_wilson|Clark-Wilson]] (integrita)

- **CDI** (Constrained Data Item) – data, jejichž integritu chráníme
- **UDI** (Unconstrained Data Item) – ostatní data (např. uživatelský vstup)
- **TP** (Transformation Procedure) – naprogramované operace udržující integritu CDI
- **IVP** (Integrity Verification Procedure) – kontrola platnosti CDI

Další modely (jen zmíněny): Brewer-Nash, Goguen-Meseguer, Sutherland, Graham-Denning, Harrison-Ruzzo-Ullman.


## [[defense_in_depth|Defense in Depth]]

Víceúrovňové zabezpečení – pokud selže jedna vrstva ochrany, chrání další. Analogie: zamčená zásuvka → místnost → byt → budova → kamery. Jiná analogie: **opevněný hrad** – obránci mají více obranných zdí, pokud útočník prorazí jednu, čeká ho hned další obranná linie.

- **Žádná jednotlivá vrstva** ochrany není spoléhaná sama o sobě
- Cíl: **minimalizovat dopad** bezpečnostního incidentu, ne spoléhat na jednu neprůstřelnou bariéru
- Vyžaduje **koordinaci napříč všemi vrstvami**

### Vrstvy v praxi

Koncept má **šest vrstev** – od nejširší (bezpečnostní politiky) až po tu nejvnitřnější a nejcennější (data). Každá vrstva chrání to, co je pod ní.

1. **Bezpečnostní politiky a lidský faktor** – řízení rizik (identifikace a odstranění chybných dat či hrozeb), pravidla pro hesla a **BYOD** (vlastní zařízení), bezpečnostní audit, školení zaměstnanců – osvěta mění nejslabší článek v obranu; politika je nějaké pravidlo

2. **Fyzická bezpečnost** – **biometrie a ID karty** (ověření identity při vstupu do budovy), **kamery a hlídky** (nepřetržitý dohled), **ploty, mříže, zámky** (fyzické překážky proti vniknutí)

3. **Síťová bezpečnost** – firewall (blokuje nežádoucí síťový provoz), IDS (systém detekce pohybu) / IPS (to co zjisti IDS tak na to reaguje ze tomu zabráni), **segmentace** (oddělení citlivých dat), **SIEM** (monitoring v reálném čase), **ACL**

4. **Bezpečnost zařízení** – **aktualizace OS** (pravidelné záplaty), přístupová oprávnění (ověření identity a role uživatele), **auditování a blokace USB** (kontrola aktivit, zákaz neautorizovaných zařízení)

5. **Bezpečnost aplikací** – **bezpečné kódování** (aplikace odolné vůči útokům již od návrhu), **WAF** (Web Application Firewall), pravidelné záplaty (rychlé odstranění známých zranitelností)

6. **Bezpečnost dat** – **šifrování** (data čitelná pouze s odpovídajícím klíčem), **zálohování** (obnova dat po ztrátě nebo útoku)

**Průřezově – správa přístupu a identit:** autentizace a autorizace (ověření kdo jste a co smíte dělat), **vícefaktorová autentizace (MFA)** – heslo + potvrzení (klíč, telefon, biometrie).

**Bezpečnostní monitorování a reakce** – SIEM, logování, incident response.

### Příklad: datacentrum Google (6 fyzických vrstev)

1. **hranice pozemku** (100 % plochy) – jasné značení a perimetrální oplocení
2. **bezpečný obvod** – hlavní vstupní brána, chytré oplocení, kamery a fyzické hlídky 24/7
3. **přístup do budovy** – eliminace neoprávněných identit: nutnost ID karty zkombinované se **skenem duhovky**
4. **Security Operations Center (SOC)** – monitorovací mozek operující 24/7, 365 dní v roce
5. **základna datacentra** – přístup povolen pro **méně než 1 % zaměstnanců**, vstupují výhradně technici provádějící aktivní údržbu
6. **"tajemná vrstva"** – nejvíce střežený bod, kam vstupuje absolutní minimum určených techniků za jediným účelem: **fyzická likvidace a mazání pevných disků**

### Datové centrum vs. zdravotnické zařízení

Defense in Depth se nasazuje jinak podle toho, co organizace chrání:

| Datové centrum | Zdravotnické zařízení |
| :-- | :-- |
| rozsáhlá ochrana široké škály IT zdrojů | ochrana citlivých **pacientských dat** |
| pokročilá síťová **segmentace** | důraz na **soulad s předpisy** |
| robustní monitoring a reakce na incidenty | šifrování dat a přístup jen pro zdravotnický personál |

V obou případech platí též: **bez proškolených lidí žádná vrstva obrany nefunguje spolehlivě.**

## ISO/IEC 19249

### Architektonické principy

- **Oddělení domén** – komponenty seskupené podle společných bezpečnostních atributů (např. úrovně oprávnění procesoru)
- **Vrstvení** – bezpečnost zaváděná na více úrovních systému (např. model OSI)
- **Zapouzdření** – skrytí nízkoúrovňové implementace, přístup jen přes definované metody/API
- **Redundance** – zajišťuje dostupnost a integritu (např. RAID, záložní zdroj)
- **Virtualizace** – sdílení hardwaru mezi více systémy, sandboxing

### Principy návrhu

- **[[nejmensi_privilegium|Nejmenší privilegium]]** – přístup jen v míře nutné pro danou úlohu
- **[[minimalizace_utocneho_povrchu|Minimalizace útočného povrchu]]** – vypnout vše nepotřebné
- **Centralizované ověřování parametrů** – validace vstupů na jednom místě
- **Centralizované bezpečnostní služby** – např. jeden centrální autentizační server
- **Příprava na chyby a výjimky** – systém musí bezpečně selhat (např. firewall při selhání blokuje, nepropouští)



## Princip nejnižších oprávnění (Least Privilege) – podrobně

Omezení přístupových práv uživatelů a programů na nejnižší úroveň stále slučitelnou s jejich úlohou. Cíl: minimalizovat dopad neoprávněných akcí nebo útoků. Příklad rizika při porušení: Edward Snowden měl příliš vysoká oprávnění, což mu umožnilo získat a zveřejnit citlivá data NSA.

### Základní myšlenka

- heslo principu: **„potřebuje → dostane, nepotřebuje → nemá“**
- omezuje se **co** (zdroje, operace, data), **kdy** (čas) i **v jaké roli**
- týká se **všech subjektů**, nejen lidí: uživatel, aplikace, proces, služba, [[administrator|administrátor]]
- nejde o odstranění všech útoků, ale o **menší útočnou plochu a menší dopad** incidentu

### Standardní uživatel vs. administrátor

| [[standardni_uzivatel\|Standardní uživatel]] | [[administrator\|Administrátor]] |
| :-- | :-- |
| web, e-mail, dokumenty, běžné aplikace | instalace, konfigurace, správa účtů, bezpečnostní nastavení |
| **nesmí** měnit systémové soubory ani spravovat účty | vyšší práva jen tehdy, když jsou potřeba |

- **běžná práce ≠ administrace** → běžný účet + oddělená administrace + řízené zvýšení práv + audit
- **stejný útok, jiný dopad:** napadený admin = změny konfigurace, přístup k dalším datům, větší škody; napadený standardní uživatel = omezený přístup a **snazší izolace**

### Řízení přístupu v operačním systému

- oprávnění se řeší na úrovni **uživatele, procesu, souboru a služby**
- postup: **[[identifikace]]** (kdo jsem) → **[[autentizace]]** (ověření) → **[[autorizace]]** (co smím) → **oprávnění**
- příklad: `student.txt` → Matyáš: čtení + zápis, učitel: jen čtení, ostatní: žádný přístup

### Technická realizace

- **[[rbac|RBAC]] (Role-Based Access Control)** – oprávnění navázaná na roli, ne na konkrétního uživatele; politika zůstává stabilní i při personálních změnách
- **[[lua|LUA]] (Least Privilege User Accounts)** – běžné účty s omezenými právy, vyšší oprávnění (admin) jen dočasně a na vyžádání
- **[[sandboxing|Sandboxing]]** – izolace aplikace v "pískovišti", omezený přístup k systémovým zdrojům
- **[[pam|PAM]] (Privileged Access Management)** – řízení, monitorování a audit privilegovaného přístupu
- minimální instalace software, centralizované přístupové kontroly a monitorování, automatizace přidělování oprávnění
- příklad RBAC (nemocnice): **lékař** – zdravotní dokumentace a výsledky vyšetření; **sestra** – jen potřebné údaje pacienta; **administrativa** – objednávky a fakturace. Role místo jednotlivců = jednodušší správa a konzistentní pravidla

### Dočasná oprávnění (JIT) a UAC

- **[[jit|JIT]] (Just-in-Time)** – oprávnění jen na dobu úkolu: žádost → ověření → dočasné oprávnění → úkol → **automatické odebrání**. Admin tak není adminem celý den → kratší okno pro zneužití, lepší audit, menší dopad kompromitovaného účtu
- **[[uac|UAC]] (User Account Control, Windows)** – uživatel běží jako standardní; při potřebě vyšších práv systém vyžádá **potvrzení nebo přihlašovací údaje**. Vyšší práva jen pro konkrétní úkol (instalace, změna nastavení)
- oprávnění je třeba **průběžně revidovat** – role, systémy i potřeby se mění (princip není jednorázové nastavení)

### Kroky zavedení v organizaci

1. analýza a identifikace požadavků (inventarizace systémů, rolí a potřeb přístupu)
2. definice přístupových politik (zavedení RBAC)
3. minimalizace oprávnění uživatelů i aplikací
4. pravidelná revize a aktualizace oprávnění
5. školení zaměstnanců
6. technologická podpora (nástroje pro správu identit – [[iam|IAM]])
7. monitorování a audit přístupu

### Případová studie – fakultní nemocnice

Problém: lékaři, sestry i administrativa měli stejnou úroveň přístupu k EHR (elektronickým zdravotním záznamům), což zvyšovalo riziko zneužití dat a komplikovalo audit.

Řešení: rozdělení uživatelů podle role, přiřazení odpovídajících přístupových práv (např. sestry bez přístupu k finančním údajům), nasazení [[iam|IAM]] nástrojů, pravidelné audity a školení.

Výsledek: vyšší bezpečnost dat, lepší auditovatelnost, nižší riziko úniku.

## Důvěra

- **Trust but Verify (důvěřuj, ale prověřuj)** – i důvěryhodné entitě se ověřuje chování (logování, IDS/IPS)
- **[[zero_trust|Zero Trust]] (nulová důvěra)** – důvěra = zranitelnost; "nikdy nedůvěřuj, vždy ověřuj". Žádné zařízení není důvěryhodné jen díky umístění/vlastnictví, ověření se vyžaduje před každým přístupem
  - **[[mikrosegmentace|Mikrosegmentace]]** – síť rozdělena na malé segmenty (třeba i jeden hostitel), komunikace mezi nimi vyžaduje autentizaci

## Model sdílené odpovědnosti (cloud)

Bezpečnost v cloudu je rozdělená mezi poskytovatele a zákazníka podle typu služby:

- **IaaS** – zákazník má plnou kontrolu (a odpovědnost) nad operačním systémem
- **SaaS** – zákazník nemá přímý přístup k operačnímu systému, odpovědnost je hlavně na poskytovateli

## Zdroj

TryHackMe – *Principy kybernetické bezpečnosti*; Kříž, P. (2018). *Kybernetická bezpečnost*. CZ.NIC.
