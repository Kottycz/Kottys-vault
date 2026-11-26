---
aliases: [DHCP teorie, Jak funguje DHCP]
tags: [ops, teorie]
---

# DHCP – jak počítače dostávají adresy automaticky

Škola vybavila učebnu patnácti počítači. Kdyby správce zadával [[IP adresa|IP]] ručně, trvalo by to dlouho a stačí jeden překlep → dvě zařízení se **stejnou adresou** → obě odpovídají na provoz toho druhého a síť přestane fungovat. Při každé změně (nová brána, jiný [[DNS]]) by se musel obejít každý počítač. Řešení je **[[DHCP]] server**: počítač se při připojení sám zeptá, jakou adresu a nastavení má mít, a server mu je **půjčí** na omezenou dobu. Nepoužité adresy se tak vracejí zpět do zásoby.
Praxe: [[02_DHCP]] · Pojmy: [[DHCP]], [[DHCP scope]], [[DORA]], [[lease]]

> **Jako půjčovna kol:** zákazník nepřijde s vlastním kolem, ale řekne, že nějaké potřebuje. Půjčovna mu na čas jedno přidělí (adresa), řekne pravidla (brána, [[DNS]]) a po čase si ho vezme zpět, nebo zápůjčku prodlouží.

---

## Pojmy

| Pojem | Význam |
| :-- | :-- |
| **[[DHCP]] server / klient** | server adresy přiděluje (SRV1-DC), klient je žádá (PC1-WIN) |
| **scope** | rozsah adres, ze kterého server přiděluje (`.100–.200`) |
| **lease (zápůjčka)** | doba, na kterou je adresa půjčená |
| **exclusion** | adresy uvnitř scope, které server nikdy nepřidělí |
| **rezervace** | pevná adresa pro konkrétní zařízení podle [[MAC adresa\|MAC]] adresy |
| **options** | další údaje k adrese: brána, [[DNS]] server, doména |
| **broadcast / unicast** | zpráva všem v síti / jednomu příjemci |
| **[[APIPA]]** | adresa `169.254.x.x`, kterou si Windows dá sám, když [[DHCP]] neodpoví |
| **autorizace** | povolení [[DHCP]] serveru v [[AD DS\|AD]], bez kterého v doméně neodpovídá |
| **rogue [[DHCP]]** | falešný, neautorizovaný [[DHCP]] server |

## Jak DHCP funguje – DORA

[[DHCP]] běží nad **[[UDP]]**: server poslouchá na portu **67**, klient na **68**. Přidělení má čtyři kroky – podle začátečních písmen **[[DORA]]**:

| Krok | Zpráva | Směr | Doručení | [[IP adresa\|IP]] zdroj → cíl |
| :-- | :-- | :-- | :-- | :-- |
| 1 | **Discover** | klient → server | broadcast | `0.0.0.0` → `255.255.255.255` |
| 2 | **Offer** | server → klient | broadcast nebo unicast | server → `255.255.255.255` / nabízená [[IP adresa\|IP]] |
| 3 | **Request** | klient → server | broadcast | `0.0.0.0` → `255.255.255.255` |
| 4 | **Acknowledge** | server → klient | broadcast nebo unicast | server → `255.255.255.255` / přidělená [[IP adresa\|IP]] |

- **[[broadcast]]** jde všem v síti – na Ethernetu cílová [[MAC adresa|MAC]] `ff:ff:ff:ff:ff:ff`, v [[IP adresa|IP]] `255.255.255.255`
- **[[unicast]]** jde jednomu – server ho pošle přímo na [[MAC adresa|MAC]] klienta, protože klient ještě nemá platnou [[IP adresa|IP]]

### Co se děje v jednotlivých krocích

1. **Discover – „hledám [[DHCP]] server“.** Klient nemá žádnou [[IP adresa|IP]], proto jako zdroj používá `0.0.0.0`. Neví, kde server je, takže musí poslat **broadcast**. Zprávu dostanou všichni, odpoví jen [[DHCP]] servery. Nese [[MAC adresa|MAC]] klienta a náhodné číslo transakce **xid**, podle kterého klient pozná, že odpověď patří jemu.
2. **Offer – „nabízím ti adresu“.** Každý server, který zprávu slyšel, vybere ze scope volnou adresu, **dočasně ji pro klienta rezervuje** a pošle ji s maskou, délkou lease a options. Jestli půjde broadcastem nebo unicastem, určuje příznak (flag) v Discoveru – klient v něm říká, jestli umí přijmout unicast ještě před nastavením [[IP adresa|IP]].
3. **Request – „beru tuhle nabídku“.** Klient si vybere jednu nabídku (většinou první) a odpoví **broadcastem**, i když už ví, který server si vybral. Důvod: zpráva obsahuje identifikaci vybraného serveru a **ostatní servery se z ní dozví**, že jejich nabídka neprošla, a uvolní rezervovanou adresu.
4. **Acknowledge – „platí, adresa je tvoje“.** Server zapíše zápůjčku do databáze (**Address Leases**) a pošle konečné hodnoty. Klient si adresu nastaví. Může ještě přes **[[ARP]]** ověřit, že ji nikdo jiný nepoužívá – když ano, pošle **[[DHCP]] Decline** („adresa je obsazená“) a začne znovu s jinou.

## Životní cyklus lease

Adresa se nepůjčuje natrvalo. Klient ji obnovuje **postupně**, ne až na konci:

| Kdy | Co klient udělá | Typ |
| :-- | :-- | :-- |
| **50 % doby ([[lease\|T1]])** | pošle Request serveru, který mu adresu dal; ten odpoví Ack a lease se prodlouží | unicast |
| **87,5 % doby ([[lease\|T2]])** | původní server neodpověděl → Request **kterémukoli** serveru | broadcast |
| **vypršení** | adresu přestane používat, začne znovu od Discover | broadcast |

- příklad: lease **8 dní** (výchozí ve Windows Serveru) → první pokus po **4 dnech**, druhý po **7 dnech**
- **[[DHCP]] [[DORA|NAK]]** – server žádost odmítne (např. klient chce obnovit adresu z jiné sítě) → klient začne od Discoveru
- **[[DHCP]] Release** – klient adresu vrátí dřív (unicast)
- příkazy: `ipconfig /release` (pošle Release), `ipconfig /renew` (získá nebo obnoví adresu)

## Když DHCP server neodpovídá – APIPA

Když klient na Discover nedostane odpověď, Windows si dá **[[APIPA]]** adresu z rozsahu **`169.254.0.0/16`**. Zvolí ji náhodně, přes [[ARP]] ověří, že je volná, a každých pár minut zkouší [[DHCP]] znovu.

Adresa `169.254.x.x` je proto **spolehlivý příznak problému**: klient je v síti, ale [[DHCP]] mu neodpověděl. Typické příčiny:

- [[DHCP]] server neběží nebo **není autorizovaný** v doméně
- scope **není aktivovaný**
- scope je **vyčerpaný** (žádná volná adresa)
- klient a server jsou **v jiné síti** a mezi nimi není **[[DHCP relay]]**, který by broadcast přeposlal

[[APIPA]] adresa nemá bránu ani [[DNS]] → funguje jen v místní síti. Chybu hledej na straně serveru.

## Scope, exclusion, rezervace a options

- **[[DHCP scope]]** – rozsah, ze kterého server přiděluje (u nás `.100–.200`); servery mají adresy mimo něj (`.10`, `.20`, `.30`), takže nikdy nedostanou adresu klienta
- **exclusion** – adresy **uvnitř** scope, které server nepřidělí (např. zařízení s ručně nastavenou adresou uvnitř rozsahu); adresy mimo scope se vylučovat nemusí, ty server nepřiděluje vůbec → v modulu žádné nepřidáváme
- **rezervace** – pevná adresa pro konkrétní zařízení podle [[MAC adresa|MAC]]; zařízení pořád používá [[DHCP]], ale dostane vždy stejnou adresu (tiskárna `.150`)
- **options** – údaje přidávané k adrese:
  - **003** Router – výchozí brána
  - **006** [[DNS]] Servers
  - **015** [[DNS]] Domain Name
- options jdou nastavit na **serveru** (pro všechny scope), na **scope** a na **rezervaci**; **konkrétnější úroveň vyhrává**

### Proč autorizace (rogue DHCP)

- klient **věří první nabídce**, která dorazí
- kdyby si kdokoli spustil vlastní [[DHCP]] server (omylem domácí router zapojený do učebny, nebo útočník), mohl by klientům dát **špatnou bránu nebo [[DNS]]** a přesměrovat jejich provoz = **[[rogue DHCP]]**
- **autorizace v [[AD DS|AD]]** zajistí, že [[DHCP]] role na Windows Serveru v doméně začne odpovídat jen tehdy, když ji tam povolil správce (u nás průvodce *Complete [[DHCP]] configuration*)

### Proč jsou v options DNS a doména

- klient v doméně musí najít řadič – a hledá ho přes **[[DNS]]** ([[SRV záznam|SRV]] záznamy, viz [[01c_Jmeno_domeny_a_DNS]])
- proto [[DHCP]] předává i **[[DNS]] server (006)** a **jméno domény (015)**; bez nich by klient adresu měl, ale do domény by se nepřihlásil
- **pozor:** průvodce může nabídnout i adresu **internetové karty** serveru – ta v [[DNS]] options být nesmí, klienti by dostali [[DNS]] server, který o doméně neví

## Jak komunikaci vidět

- **klient:** `ipconfig /all` → *[[DHCP]] Enabled*, *[[DHCP]] Server*, *Lease Obtained*, *Lease Expires*
- **server:** [[DHCP]] konzole → **Address Leases** (všechny zápůjčky i s [[MAC adresa|MAC]])
- **[[Wireshark]]** na klientovi: filtr `dhcp` (nebo `udp.port == 67 or udp.port == 68`), pak `ipconfig /release` a `/renew` → uvidíš všechny čtyři zprávy [[DORA]] s adresami a porty

## U nás

- [[DHCP]] role na **SRV1-DC**, autorizovaná v doméně
- scope **Ucebny-Klienti** `192.168.16.100–200`, maska `255.255.255.0`, lease 8 dní
- options: brána `192.168.16.1` (003), [[DNS]] `192.168.16.10` (006), doména `kotrba.cyberschool.internal` (015)
- rezervace pro tiskárnu `192.168.16.150`
- ověření na PC1-WIN: `ipconfig /release`, `/renew`, `/all` a v konzoli *Address Leases*
- [[DHCP]] je na řadiči kvůli jednoduchosti (méně strojů, snadná autorizace); v praxi by se řadič nepřetěžoval
