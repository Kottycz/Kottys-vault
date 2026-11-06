# Aplikační vrstva

## Session layer

Funkce na relační vrstvě vytvářejí a udržují dialogy mezi zdrojovou a cílovou aplikací. Relační vrstva zpracovává výměnu informací pro zahájení dialogů, jejich udržení v aktivním stavu a restartování relací, které jsou přerušeny nebo delší dobu nečinné.

## Presentation layer

- Formátování neboli prezentace dat na zdrojovém zařízení do kompatibilního formátu pro příjem cílovým zařízením.
- Komprese dat způsobem, který může cílové zařízení dekomprimovat.
- Šifrování dat pro přenos a dešifrování dat po přijetí.

## Protokoly aplikační vrstvy

**[[DNS]]** – systém doménových jmen. [[TCP]], [[UDP]] 53. Překládá názvy domén (např. cisco.com) na [[IP adresa|IP adresy]].

**[[DHCP]]** – Dynamic Host Configuration Protocol. UDP client 68, server 67. Dynamicky přiděluje IP adresy pro opětovné použití, když už nejsou potřeba.

**[[SMTP]], [[POP3]], [[IMAP]]** – e-mailové služby.

**[[HTTP]]** – protokol pro přenos hypertextu. TCP 80, 8080. Soubor pravidel pro výměnu textu, grafiky, zvuku, videa a dalších multimediálních souborů na World Wide Webu.

**[[HTTPS]]** – zabezpečený HTTP. TCP, UDP 443. Prohlížeč používá šifrování k zabezpečení HTTP komunikace, ověřuje webovou stránku, ke které se připojujete.

## Peer-to-Peer

### Model klient – server

Klient/server model a procesy, které se nacházejí v aplikační vrstvě.

### Peer-to-Peer sítě

V [[peer-to-peer|P2P]] síti jsou dva nebo více počítačů propojeny prostřednictvím sítě a mohou sdílet zdroje.

## Web and email protocols

### HTTP / HTTPS

Pro bezpečnou komunikaci přes internet se používá protokol HTTP Secure ([[HTTPS]]). HTTPS používá ověřování a šifrování ([[TLS]]) k zabezpečení dat při jejich přenosu mezi klientem a serverem.

### E-mailové protokoly

E-mailoví klienti komunikují s poštovními servery za účelem odesílání a přijímání e-mailů. Poštovní servery komunikují s jinými poštovními servery za účelem přenosu zpráv z jedné domény do druhé. E-mailový klient při odesílání e-mailů nekomunikuje přímo s jiným e-mailovým klientem – oba klienti se spoléhají na poštovní server pro přenos zpráv.

E-mail podporuje tři protokoly: [[SMTP]], [[POP3]] a [[IMAP]]. Odesílání pošty používá SMTP. Klient načítá e-maily pomocí POP nebo IMAP.

**1. [[SMTP]] (Simple Mail Transfer Protocol)**
- Účel: výhradně odesílání e-mailů (od klienta na server a mezi servery navzájem).
- Porty: 25 (původní, dnes často blokovaný kvůli spamu), 465 (šifrovaný – SMTPS), 587 (moderní standard se šifrováním [[TLS|STARTTLS]]).
- Jak funguje: po kliknutí na „Odeslat" se e-mail pomocí SMTP doručí na odchozí poštovní server, ten pak vyhledá cílový server adresáta a zprávu mu předá.
- Přirovnání: poštovní schránka + poštovní auto, které odváží dopisy na hlavní poštu.

**2. [[POP3]] (Post Office Protocol version 3)**
- Účel: stahování e-mailů ze serveru do zařízení uživatele.
- Porty: 110 (nešifrovaný), 995 (šifrovaný – POP3S).
- Jak funguje: připojí se ke schránce, stáhne nové zprávy do zařízení a ze serveru je standardně smaže. E-maily jsou uložené lokálně.
- Výhody: dostupné offline, nezaplňují kapacitu na serveru.
- Nevýhody: nevhodné pro víc zařízení – co je stažené do PC, v mobilu už není. Při rozbití disku o e-maily přijdete.
- Přirovnání: klasická poštovní schránka na domě – pošťák hodí dopis, vezmete si ho domů a ve schránce nic nezbyde.

**3. [[IMAP]] (Internet Message Access Protocol)**
- Účel: prohlížení a správa e-mailů přímo na serveru.
- Porty: 143 (nešifrovaný), 993 (šifrovaný – IMAPS).
- Jak funguje: na rozdíl od POP3 e-maily nestahuje trvale, jen synchronizuje stav. Zůstávají uložené na serveru, v zařízení vidíte „zrcadlo" toho, co je na serveru.
- Výhody: přístup z mobilu, notebooku i webu současně, všude stejný stav schránky. Při ztrátě telefonu o e-maily nepřijdete.
- Nevýhody: potřeba stálé připojení k internetu, zaplňuje úložiště na serveru.
- Přirovnání: sdílený dokument na cloudu (Google Docs) – všichni vidí stejný soubor, změna je vidět okamžitě.

## Protokol dynamické konfigurace hostitele ([[DHCP]])

DHCP pro [[IPv4]] automatizuje přiřazování IPv4 adres, masek podsítě, bran a dalších síťových parametrů (dynamické adresování). Alternativa je statické adresování – správce zadává IP adresy ručně.

Když se hostitel připojí k síti, kontaktuje DHCP server a vyžádá si adresu. Server vybere adresu z nakonfigurovaného rozsahu (pool) a přiřadí (pronajme) ji hostiteli.

Ve větších sítích nebo tam, kde se počet uživatelů často mění, se DHCP upřednostňuje před statickým adresováním – je efektivnější než ruční konfigurace každého připojení.

DHCP může přidělovat IP adresy na konfigurovatelné časové období – **doba pronájmu (lease time)**.

**DHCP Operations** ([[DORA]]) – zpráva o nabídce (OFFER) obsahuje: adresu IPv4 a [[maska podsítě|masku podsítě]], adresu IPv4 [[DNS]] serveru, adresu IPv4 [[default gateway|výchozí brány]].

## File Transfer Protocol ([[FTP]])

FTP byl vyvinut pro přenos dat mezi klientem a serverem. FTP klient je aplikace běžící na počítači, používaná k odesílání a stahování dat z FTP serveru.
