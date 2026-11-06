# Příběh: CyberSchool — gymnázium a průmyslovka

> Verze: 2026-10-03

Všechny moduly tohoto projektu se odehrávají v jednom společném příběhu. Používejte ho jako kontext při psaní vlastní dokumentace — každý krok, který děláte, dělá **někdo konkrétní pro konkrétní důvod**, ne "protože to tak velí zadání".

## Škola

**CyberSchool — Gymnázium a Střední průmyslová škola elektrotechniky a informatiky** je středně velká škola se čtyřmi obory:

| Obor | Délka studia | Zkratka (OU / skupina) |
|---|---|---|
| Osmileté gymnázium | 8 let (prima–oktáva) | `Gymnazium-8lete` / `GG_Studenti_G8` |
| Čtyřleté gymnázium | 4 roky | `Gymnazium-4lete` / `GG_Studenti_G4` |
| Elektrotechnika | 4 roky | `Elektrotechnika` / `GG_Studenti_EL` |
| Informatika | 4 roky | `Informatika` / `GG_Studenti_IT` |

Žáky v doméně třídíme **podle oborů**, ne podle ročníků — obory se liší výukou, učebnami i tím, co žáci na počítačích potřebují; ročník se mění každý rok a správa by se jen zbytečně komplikovala.

Škola má počítačové učebny, sborovnu, kabinety, vedení a sekretariát. Dosud ale neměla žádnou centrální IT infrastrukturu:

- Každý počítač měl jen lokální účty (`student` / `student`, `ucitel` / `ucitel` na všech PC stejně).
- Hesla se sdílela na papírku nalepeném u monitoru.
- Učitelé si materiály posílali e-mailem nebo nosili na flash disku.
- Tiskárna v kabinetu se připojovala ručně na každém počítači zvlášť.
- Nikdo přesně nevěděl, kdo má k čemu přístup.

Vedení školy pověřilo žáka 4. ročníku oboru Informatika, aby jako **praktický maturitní/školní projekt** postavil školní IT infrastrukturu od nuly — a zdokumentoval ji tak, aby ji po něm mohl převzít někdo jiný.

## Postavy (uživatelé, pro které to stavíte)

| Jméno | Role | Účet | Poznámka |
|---|---|---|---|
| **Jiří Pečlivý** | správce IT (postava příběhu) | vestavěný účet `Administrator` | staví a spravuje celou infrastrukturu — viz poznámka níže |
| **Jana Nováková** | učitelka informatiky | `jana.teacher` | zadavatelka požadavků, „product owner“ příběhu, členka PK Informatika |
| **Petr Dvořák** | učitel matematiky | `petr.teacher` | běžný učitel, nechce se starat o techniku, člen PK Matematika |
| **Karel Dlouhý** | ředitel školy | `karel.zamestnanec` | vedení školy, potřebuje složku `Vedeni` a volnější pravidla než učitelé |
| **Marie Kučerová** | hospodářka / sekretariát | `marie.zamestnanec` | administrativa, tisk vysvědčení a smluv, potřebuje přístup ke složce `Smernice` a `THP` |
| **Lucie Horáková** | žákyně osmiletého gymnázia | `lucie.student` | obor Gymnázium 8leté |
| **Ondřej Malý** | žák osmiletého gymnázia | `ondrej.student` | obor Gymnázium 8leté |
| **Adam Beneš** | žák čtyřletého gymnázia | `adam.student` | obor Gymnázium 4leté |
| **Klára Veselá** | žákyně čtyřletého gymnázia | `klara.student` | obor Gymnázium 4leté |
| **Tomáš Král** | žák oboru Elektrotechnika | `tomas.student` | odevzdává úkoly, tiskne referáty |
| **Eva Svobodová** | žákyně oboru Informatika | `eva.student` | pracuje v učebně informatiky |

**Schéma účtů:** `jmeno.student`, `jmeno.teacher`, `jmeno.zamestnanec`, kde `jmeno` je **křestní jméno bez diakritiky** (Tomáš → `tomas`, Ondřej → `ondrej`). Přípona role v názvu účtu je ve výukovém prostředí záměrná: při testování oprávnění na první pohled vidíte, jestli je přihlášený žák, učitel nebo zaměstnanec. Plné přihlašovací jméno (UPN) je pak např. `eva.student@prijmeni.cyberschool.internal`. Každé křestní jméno je v příběhu jen jednou, aby se účty nepletly.

> **Vaše doména:** ve vlastní dokumentaci za `prijmeni` dosaďte své příjmení bez diakritiky, malými písmeny — např. `novak.cyberschool.internal`. `cyberschool.internal` je společný „jmenný prostor školy“, vaše příjmení odliší váš les od lesů spolužáků. Proč zrovna `.internal` a ne `.local` nebo `.lab`, vysvětluje [[Modul 1 Domain Controller/cast0#6. Jak pojmenovat doménu|Modul 1, Část 0]].

### Poznámka ke správci IT a účtu Administrator

**Jiří Pečlivý** je v příběhu jediný IT pracovník malé střední školy — přesně jako v realitě spousty menších škol, kde na správu IT infrastruktury nemá vedení rozpočet na víc než jednoho člověka. V praxi to znamená, že **veškerou administraci v tomto vzorovém postupu provádíte pod vestavěným účtem `Administrator`** (heslo `Pa55w.rd`), ne pod nějakým jeho osobním doménovým účtem typu `jiri.peclivy`. Jiří jako postava tento vestavěný účet jen "obsluhuje" — nemá založený vlastní pojmenovaný administrátorský účet.

> **Bonus na zamyšlení (nad rámec tohoto vzorového postupu):** V opravdu zralém prostředí je lepší praxí mít pro každého administrátora **vlastní pojmenovaný účet** (např. `jiri.peclivy-adm`) s delegovanými oprávněními jen na to, co skutečně potřebuje (princip nejnižších oprávnění), a vestavěný `Administrator` používat jen výjimečně (např. při obnově ze zálohy). U jedné osoby spravující malou školu je ale použití vestavěného účtu běžné a pro účely tohoto projektu dostačující — delegování rolí si můžete zkusit jako rozšíření nad rámec zadání.

### Poznámka k serverům

Oba servery — **SRV1-DC** i **SRV2-FS** — se instalují jako **Windows Server s Desktop Experience** (grafické rozhraní se Server Managerem), nikdy jako Server Core. Pro výukový projekt je důležitější, abyste viděli a chápali jednotlivé kroky v GUI konzolích (Server Manager, ADUC, DNS Manager, DHCP Manager, Print Management...), než abyste šetřili pár set MB na disku, které by ušetřila instalace Server Core.

## Technické zasazení (pro vzorový postup)

| Prvek | Hodnota |
|---|---|
| VLAN | `200` |
| Síť | `192.168.200.0/24` |
| Doména (AD) | `prijmeni.cyberschool.internal` (např. `novak.cyberschool.internal`), NetBIOS `PRIJMENI` (např. `NOVAK`) |
| SRV1-DC | `192.168.200.10` — řadič domény, DNS, DHCP |
| SRV2-FS | `192.168.200.20` — souborový, tiskový a FTP server |
| (rezerva) | `192.168.200.30` — pro budoucí rozšíření (dodatečný řadič domény SRV3-DC — v projektu jen teorie) |
| PC1-WIN | `192.168.200.100` — klient, učebna informatiky |
| Heslo (všechny účty) | `Pa55w.rd` |

## Jak se příběh vine moduly

Každý modul řeší jeden konkrétní problém, který škole ještě chybí:

1. **Domain Controller** — škola nemá centrální evidenci uživatelů, každý PC je "sám za sebe".
2. **DHCP** — nová učebna má 15 počítačů a nikdo nechce nastavovat IP adresu ručně na každém.
3. **DNS** — jména serverů a služeb se musí v síti spolehlivě najít.
4. **Active Directory** — učitelé, zaměstnanci a žáci všech čtyř oborů potřebují reálné účty, PC1-WIN musí být v doméně.
5. **Group Policy** — žáci nesmí měnit nastavení počítačů, učitelé potřebují jiná pravidla než žáci.
6. **File Server a Storage** — potřeba spolehlivého úložiště pro materiály a úkoly, které nezmizí při pádu jednoho disku.
7. **File a FTP Services** — sdílené složky pro učitele/žáky a možnost nahrát/stáhnout soubory i zvenčí školy.
8. **Print Services** — sborovna, učebna informatiky a gymnaziální učebna potřebují sdílené tiskárny bez ručního nastavování na každém PC; každý obor tiskne ve své učebně.

Na konci celého projektu předáváte škole **fungující, zdokumentovanou infrastrukturu** — přesně to popisuje [[__zadani|Co má být na konci a jak to vypadá]] a jak si to ověřit [[_vysledek|Jak se pozná, že už to mám]].
