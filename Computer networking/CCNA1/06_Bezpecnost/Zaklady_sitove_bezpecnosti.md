# Základy síťové bezpečnosti

Vetřelci mohou získat přístup k síti prostřednictvím softwarových zranitelností, hardwarových útoků nebo uhádnutím uživatelského jména a hesla někoho jiného. Vetřelci, kteří získají přístup úpravou softwaru nebo zneužitím softwarových zranitelností, se nazývají **útočníci**.

Poté, co útočník získá přístup k síti, mohou nastat čtyři typy hrozeb.

- **Krádež informací** je vloupání do počítače za účelem získání důvěrných informací. Informace mohou být použity nebo prodány k různým účelům, například když někdo krade důvěrné informace organizace, jako jsou data výzkumu a vývoje.
- **Ztráta a manipulace s daty** je vniknutí do počítače za účelem zničení nebo změny datových záznamů. Příkladem ztráty dat je útok, který odešle virus, jenž přeformátuje pevný disk počítače. Příkladem manipulace s daty je vniknutí do systému za účelem změny informací, jako je například cena položky.
- **Krádež identity** je forma krádeže informací, kdy jsou osobní údaje odcizeny za účelem převzetí identity někoho jiného. Pomocí těchto informací může útočník získat právní dokumenty, požádat o úvěr a provádět neoprávněné online nákupy. Krádež identity je rostoucí problém, který ročně stojí miliardy dolarů.
- **Přerušení služby** brání legitimním uživatelům v přístupu ke službám, na které mají nárok. Mezi příklady patří útoky typu denial of service (DoS) na servery, síťová zařízení nebo síťová komunikační spojení.

Existují tři hlavní zranitelnosti nebo slabiny: technologické, konfigurační a bezpečnostní (procedury, směrnice).

Čtyři třídy fyzických hrozeb jsou následující:

- **Hardwarové hrozby** – Patří sem fyzické poškození serverů, routerů, přepínačů, kabelových rozvodů a pracovních stanic.
- **Environmentální hrozby** – Patří sem teplotní extrémy (příliš horko nebo příliš chladno) nebo extrémy vlhkosti (příliš vlhko nebo příliš sucho).
- **Elektrické hrozby** – Patří sem napěťové špičky, nedostatečné napájecí napětí (výpadky), nepodmíněný výkon (šum) a úplná ztráta výkonu.


## Typy malwaru

Malware je zkratka pro škodlivý software.

### Viry

Počítačový virus je typ [[malware|malwaru]], který se šíří vložením své kopie do jiného programu a jeho součástí.

### Červi

Počítačové červy jsou podobné virům v tom, že replikují funkční kopie sebe sama a mohou způsobit stejný typ škody.

### Trojští koně

Jedná se o škodlivý software, který vypadá legitimně. Uživatelé jsou obvykle oklamáni, aby jej na svých systémech načetli a spustili. Trojští koně jsou také známí tím, že vytvářejí zadní vrátka, aby uživatelům se zlými úmysly poskytli přístup do systému.

**Průzkumné útoky** – objevování a mapování systémů, služeb nebo zranitelností.

## Útoky na přístup

### Útoky na heslo

Útočníci mohou útoky na hesla provádět několika různými metodami:

- Útoky hrubou silou
- Útoky trojských koní
- Čichače paketů

### Zneužívání důvěry

Při útoku s využitím zneužití důvěryhodnosti útočník použije neoprávněná oprávnění k získání přístupu k systému, čímž potenciálně ohrozí cíl. Kliknutím na tlačítko Přehrát na obrázku zobrazíte příklad zneužití důvěryhodnosti.

### Přesměrování portu

Při útoku s přesměrováním portu útočník používá kompromitovaný systém jako základnu pro útoky proti jiným cílům.

### Muž uprostřed

Při útoku typu „man-in-the-middle" se útočník nachází mezi dvěma legitimními entitami, aby mohl číst nebo upravovat data, která si mezi nimi procházejí.

### Útoky typu odmítnutí služby

Útoky typu denial of service (DoS) jsou nejznámější formou útoku a patří k nejobtížněji eliminovatelným.

**Jak DoS útok funguje:** cílem není nic ukrást ani změnit, ale znepřístupnit službu (web, server, síťové spojení) jejím legitimním uživatelům. Útočník toho dosáhne typicky jedním ze dvou způsobů:

- **Zahlcení objemem provozu** – na cíl se pošle tolik provozu (paketů, požadavků), že cíl nebo jeho připojení k síti přestane zvládat kapacitu a legitimní požadavky se k němu už nedostanou nebo na ně nestihne odpovědět.
- **Zneužití zranitelnosti/chyby** – útočník pošle speciálně upravený paket nebo posloupnost paketů, které využijí chybu v aplikaci, protokolu nebo operačním systému cíle a shodí službu nebo celý systém (např. pád procesu, zaseknutí, vyčerpání paměti).

Typické cíle: webové servery, e-mailové servery, DNS servery, ale i síťová zařízení (routery, firewally) nebo samotná komunikační linka k poskytovateli.

**Proč se DoS tak těžko eliminuje:** provoz při útoku často vypadá jako běžné legitimní požadavky (jen v obřím množství), takže není snadné automaticky rozeznat útočníka od skutečného zákazníka. Navíc útočník může falšovat (spoofovat) zdrojovou IP adresu, takže zablokování jedné adresy nepomůže a dohledání skutečného původce je obtížné.

### DDoS útok

DDoS útok je podobný DoS útoku, ale pochází z více koordinovaných zdrojů.

**Proč se DDoS dělá z víc zdrojů:** jeden útočící počítač má omezenou šířku pásma a výpočetní výkon – proti dnešním serverům a jejich připojení to často nestačí. Řešením je pro útočníka rozložit útok na **tisíce až miliony** počítačů najednou, které o útoku ani nemusí vědět.

**Obrana proti DDoS** obvykle vyžaduje specializované služby (scrubbing centra, CDN sítě s velkou kapacitou), které dokážou rozeznat a odfiltrovat útočný provoz dřív, než dorazí k cíli – běžný firewall na hranici vlastní sítě sám o sobě proti velkému DDoS útoku nestačí.



## Zmírnění síťových útoků

### Uchovávání záloh

Zálohování konfigurací a dat zařízení je jedním z nejúčinnějších způsobů ochrany před ztrátou dat. Záloha dat ukládá kopii informací z počítače na vyměnitelné záložní médium, které lze bezpečně uchovávat. Zařízení infrastruktury by měla mít zálohy konfiguračních souborů a obrazů IOS na FTP nebo podobném souborovém serveru. Pokud dojde k selhání hardwaru počítače nebo routeru, lze data nebo konfiguraci obnovit pomocí záložní kopie.

### Aktualizace, upgrade a oprava

Udržování kroku s nejnovějším vývojem může vést k efektivnější obraně proti síťovým útokům. S vydáváním nového malwaru je nutné, aby podniky používaly nejnovější verze antivirového softwaru.

Nejúčinnějším způsobem, jak zmírnit útok červů, je stáhnout si bezpečnostní aktualizace od dodavatele operačního systému a opravit všechny zranitelné systémy.

### Ověřování, autorizace a účtování

Všechna síťová zařízení by měla být bezpečně nakonfigurována tak, aby přístup poskytovala pouze oprávněným osobám. Síťové bezpečnostní služby pro ověřování, autorizaci a účtování (AAA neboli „triple A") poskytují primární rámec pro nastavení řízení přístupu na síťových zařízeních.

### Firewall

Firewall je jedním z nejúčinnějších bezpečnostních nástrojů dostupných pro ochranu uživatelů před vnějšími hrozbami. Firewall chrání počítače a sítě tím, že brání nežádoucímu provozu ve vstupu do interních sítí.

- **Filtrování paketů** – Zabraňuje nebo povoluje přístup na základě IP nebo MAC adres.
- **Filtrování aplikací** – Zabraňuje nebo povoluje přístup konkrétním typům aplikací na základě čísel portů.
- **Filtrování URL adres** – Zabraňuje nebo povoluje přístup k webovým stránkám na základě konkrétních URL adres nebo klíčových slov.
- **Stavová inspekce paketů (SPI)** – Příchozí pakety musí být legitimní odpovědí na požadavky od interních hostitelů. Nevyžádané pakety jsou blokovány, pokud nejsou výslovně povoleny. SPI může také zahrnovat schopnost rozpoznávat a filtrovat specifické typy útoků, jako je například odmítnutí služby (DoS).

### Zabezpečení koncových bodů

Koncový bod neboli hostitel je individuální počítačový systém nebo zařízení, které funguje jako síťový klient. Mezi běžné koncové body patří notebooky, stolní počítače, servery, chytré telefony a tablety. Zabezpečení koncových zařízení je jedním z nejnáročnějších úkolů správce sítě, protože zahrnuje lidskou povahu. Společnost musí mít zavedeny dobře zdokumentované zásady a zaměstnanci si musí být těchto pravidel vědomi. Zaměstnanci musí být proškoleni v řádném používání sítě.

### Zabezpečení zařízení

U routerů Cisco lze k zabezpečení systému použít funkci Cisco AutoSecure, jak je znázorněno v příkladu.

```
# auto secure
```

Kromě toho existuje několik jednoduchých kroků, které by měly být provedeny a které platí pro většinu operačních systémů:

- Výchozí uživatelské jméno a heslo by měla být okamžitě změněna.
- Přístup k systémovým prostředkům by měl být omezen pouze na osoby, které jsou k jejich používání oprávněny.
- Veškeré nepotřebné služby a aplikace by měly být pokud možno vypnuty a odinstalovány.

Zařízení dodaná od výrobce často leží ve skladu delší dobu a nemají nainstalované nejaktuálnější záplaty.

### Hesla

```
service password-encryption
security passwords min-length
login block-for # attempts # within #
```

Ve výchozím nastavení se routery Cisco odhlásí z relace EXEC po 10 minutách nečinnosti. Toto nastavení však můžete snížit pomocí konfiguračního příkazu `exec-timeout minutes seconds`.

### Povolení SSH

Telnet zjednodušuje vzdálený přístup k zařízením, ale není bezpečný. Data obsažená v paketu Telnet jsou přenášena nešifrovaná. Z tohoto důvodu se důrazně doporučuje povolit na zařízeních protokol Secure Shell (SSH) pro zabezpečený vzdálený přístup.

*viz laboratorní úloha*

### Zakázání nepoužívaných služeb

Typ služeb, které jsou ve výchozím nastavení zapnuté, se bude lišit v závislosti na verzi systému IOS.

**Souvisí:** [[firewall]], [[SSH]], [[Telnet]], [[IOS]], [[MAC adresa]], [[port]], [[malware]], [[DoS-DDoS]], [[MITM]], [[AAA]], [[SPI]], [[koncový bod]]
