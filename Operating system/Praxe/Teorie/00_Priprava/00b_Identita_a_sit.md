---
aliases: [Identita a síť serveru, Hostname a IP]
tags: [ops, teorie]
---

# Jméno, adresa a účet serveru

V síti platí jednoduché pravidlo: každé zařízení musí být **jednoznačně rozpoznatelné**. Když mají dvě zařízení stejnou adresu, obě „odpovídají“ na provoz toho druhého a spojení se trhá. Když server nemá stálé jméno a adresu, nenajdou ho klienti, [[DNS]], sdílené složky ani zásady. A když nevíš, **kdo** a pod jakým účtem na serveru pracoval, nezjistíš, odkud přišla chyba. Proto se na každém stroji hned na začátku řeší tři věci: **jméno**, **adresa** a **účet správce**.
Praxe: [[00_Priprava_OS]] · Předchozí: [[00a_Virtualizace_edice_aktivace]] · Další: [[00c_Cas_jazyk_soukromi]]

> **Jako adresa domu:** ulice a číslo popisné (jméno a [[IP adresa|IP]]) musí být jedinečné, jinak pošťák nic nedoručí. A když se vchod pořád mění, přestane zvonit.

---

## Jméno počítače (hostname)

Jméno je „příjmení“ počítače v síti. Pravidla:

- **jedinečné** v síti i v doméně
- nejvýš **15 znaků** – to je limit [[NetBIOS]] jména, které Windows používá pro starší služby a v přihlášení (`KOTRBA\Administrator`)
- jen **písmena bez diakritiky, číslice a pomlčka**; žádné mezery, tečky, podtržítka a nesmí to být jen číslice
- čitelné – má prozradit **roli a pořadí**, aby správce hned věděl, co stroj dělá

| Dobře | Špatně |
| :-- | :-- |
| `SRV1-DC` (server 1, **d**omain **c**ontroller) | `server`, `test2` – nic neříká |
| `SRV2-FS` (server 2, **f**ile **s**erver) | `Jirkuv-novy-pc` – mění se s lidmi |
| `PC1-WIN` (klient 1, Windows) | `Server 1` (mezera), `kancelar_jirka` (podtržítko), `123` (jen čísla) |

**Proč hned na začátku:** na jménu závisí [[DNS]] záznamy, členství v doméně, sdílené složky i [[GPO]]. Přejmenovat řadič domény jde, ale je to složité a riskantní – proto se jméno nastaví **před povýšením** na řadič.

Po připojení do domény se ke jménu přidá doména a vznikne **[[FQDN]]**: `srv1-dc.kotrba.cyberschool.internal`.

## IP adresa a síť

### Z čeho se skládá IPv4 adresa

- [[IPv4]] adresa má 32 bitů, zapisuje se jako 4 čísla 0–255 (oktety): `192.168.16.10`
- **[[maska podsítě]]** říká, kolik bitů patří síti: `/24` = prvních 24 bitů je síť (`192.168.16`), posledních 8 bitů je zařízení
- v síti `/24` je **254** použitelných adres (`.1`–`.254`); `.0` označuje celou síť a `.255` je [[broadcast]] („všem v síti“)
- zařízení ve stejné síti spolu mluví přímo; data **mimo síť** posílají **[[default gateway|výchozí bráně]]** (routeru), která je předá dál

### Privátní adresy

- rozsahy z [[RFC]] 1918: `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`
- v internetu se nesměrují, takže je může používat kdokoli najednou
- do internetu se zařízení dostane přes router, který adresy překládá (**[[NAT]]**)
- my: `192.168.N.0/24`, kde **N = číslo pracoviště** (já **16**) → každý žák má vlastní síť a sítě spolužáků se nepletou

### Statická nebo dynamická adresa

| | **Statická** | **Dynamická ([[DHCP]])** |
| :-- | :-- | :-- |
| nastavení | ručně na každém zařízení | automaticky ze serveru |
| změna | jen když ji změníš | může se při obnovení změnit |
| správa | pracná, hrozí překlep a konflikt | pohodlná, centrální |
| pro | **servery**, tiskárny, síťové prvky | **klienty**, notebooky |

- **server musí mít stálou adresu** – ukazují na něj [[DNS]] záznamy, sdílené složky, tiskárny, zásady, pravidla firewallu; kdyby se změnila, klienti ho nenajdou
- **klienti** adresu znát předem nepotřebují → [[DHCP]] (Modul 2)
- [[DHCP]] rezervace pro servery ne – první server (SRV1-DC) je sám [[DHCP]] serverem, který teprve stavíme

### Plán adres

Než nastavíš první adresu, je dobré mít plán, kdo má jaké číslo:

| Adresa | Zařízení | Typ |
| :-- | :-- | :-- |
| `192.168.16.1` | výchozí brána (router) | statická |
| `192.168.16.10` | SRV1-DC | statická |
| `192.168.16.20` | SRV2-FS | statická |
| `192.168.16.30+` | další servery | statická |
| `192.168.16.100–200` | klienti | [[DHCP]] |

- rozsah klientů je **oddělený** od serverů → [[DHCP]] nikdy nepřidělí klientovi adresu serveru (konflikt by vznikl, kdyby dostal `.10`)

### DNS server v nastavení

- každý stroj má nastavené, **kdo mu překládá jména** → všichni používají **SRV1-DC** (`192.168.16.10`)
- SRV1-DC používá sám sebe (poběží na něm [[DNS]] s doménou – Modul 1 a 3)
- klientům ho předá [[DHCP]] spolu s adresou

## Účet správce

Windows při instalaci vytvoří vestavěný účet **`Administrator`**:

- je **vždy přítomný** a nejde smazat
- má **plná práva** nad strojem
- na Windows 11 je ve výchozím stavu **vypnutý** → zapíná se ručně

V projektu děláme všechno pod `Administrator` (heslo viz [[Rules]]) – je to zjednodušení pro výuku, správce Jiří Pečlivý je jediný IT pracovník školy. Heslo je stejné všude a platí jen ve výuce; v praxi má být **dlouhé, jedinečné pro každý stroj a ve správci hesel**.

### Jak je to v praxi

- **nepoužívá se jeden sdílený účet** – každý správce má vlastní jmenovaný účet (např. `jiri.peclivy-adm`)
- **princip nejnižších oprávnění** – každý účet má jen práva, která opravdu potřebuje
- důvod: když se pod jedním účtem přihlásí víc lidí, nezjistíš, **kdo** co udělal; vestavěný `Administrator` se používá jen výjimečně (obnova)
- proto taky do dokumentace dáváme výstupy s **promptem** (datum, čas, počítač) – viz [[00c_Cas_jazyk_soukromi]]

Po povýšení SRV1-DC na řadič (Modul 1) se z místního `Administrator` stane **doménový** `Administrator` s právy nad celou doménou – v promptu se pak místo jména počítače objeví doména: `KOTRBA\Administrator`.

## U nás

- stroje **SRV1-DC**, **SRV2-FS**, **PC1-WIN**
- servery staticky `.10` a `.20`, klienti z [[DHCP]] `.100–.200`
- brána `.1`, [[DNS]] `.10`
- správa pod vestavěným `Administrator`
