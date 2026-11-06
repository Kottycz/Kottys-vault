# Pravidla práce s vaultem

> Verze: 2026-10-03

Tento vault je vaše pracovní dokumentace k projektu **Postavte si školní IT**. Přečtěte si tato pravidla celá, než začnete — ušetří vám ztracenou práci i body.

## 1. Jak vault funguje

Vault vzniká **postupně**. Ke každému modulu dostanete nejdřív:

- `__zadani.md` — co má být na konci modulu a jak to vypadá,
- `cast0.md` — teorie k modulu,
- `_vysledek.md` — jak se pozná, že je modul hotový,
- šablony pro vaši dokumentaci ve složce `Moje dokumentace` (viz bod 3).

Postup správného řešení (`cast1.md`, `cast1-powershell.md`, …) a k němu screenshoty přibydou do složky modulu **až po kontrole vaší práce**. Na konci projektu tak budete mít celou dokumentaci infrastruktury.

Začněte [[00-pribeh-skoly|příběhem školy]] a [[__zadani|cílem celého projektu]].

## 2. První spuštění

1. Rozbalte ZIP s vaultem do složky, kde se zálohuje — doporučujeme svůj OneDrive (např. `OneDrive\OPS\Postavte si školní IT`).
2. Spusťte Obsidian a zvolte **Open folder as vault** → vyberte rozbalenou složku.
3. Nastavte přílohy podle bodu 7.

Vault s nikým nesdílejte a nepracujte ve společné složce.

## 3. Soubory od učitele × vaše vlastní práce

**Toto je nejdůležitější pravidlo.**

- Soubory v kořeni vaultu a ve složkách `Modul …` jsou **od učitele**. **Neupravujte je** — při každé aktualizaci se přepíšou a vaše úpravy zmizí. Chcete-li si do nich něco poznamenat, zkopírujte si text do své složky.
- Veškerou vlastní práci pište **jen** do složky `Moje dokumentace`, rozdělené po modulech:

```
Moje dokumentace\
└── Modul 1 Domain Controller\
    ├── postup.md      ← co jste dělali, krok za krokem
    ├── overeni.md     ← důkazy ke každému bodu z _vysledek.md
    └── images\        ← vaše screenshoty
```

### Jak vyplňovat šablony

- Každý soubor `postup.md` a `overeni.md` už obsahuje nadpisy a kolonky s **ID** (např. `M1-SRV1.V3-D1`). **Nadpisy ani ID neměňte, nemažte a nepřesouvejte** — podle nich se vaše práce porovnává se vzorovým řešením.
- Nahraďte každé `DOPLNIT` svým obsahem. Komentáře `<!-- … -->` můžete nechat, v náhledu nejsou vidět.
- **Postup** (`…P1`, `…P2`) = co jste skutečně udělali: kde jste klikli a jaké hodnoty zadali, nebo příkazy, které jste spustili — v pořadí, jak jste je prováděli.
- **Důkaz** (`…-D1`, `…-D2`) = textový výpis nebo screenshot, na kterém je vidět to, co popisuje text kolonky.
- **Otisk** (`…V0-O`) = výstup daných příkazů, viz bod 8. Nebodá se, ale je povinný.
- Hotovou položku si můžete odškrtnout (`- [x] Hotovo`) — slouží jen vám.
- Kam do své dokumentace patří vlastní screenshot, napoví i řádky „📷 **Screenshot sem:**“ v souborech od učitele.

## 4. Přidání nového modulu nebo řešení

1. Dostanete ZIP se složkou modulu (a případně se šablonami pro `Moje dokumentace`).
2. Rozbalte ho **do kořene vaultu** — složky se samy zařadí na správné místo.
3. Zeptá-li se systém na přepsání **souborů od učitele** (kořen, složky `Modul …`), zvolte **ano** — jde o novější verzi.
4. Soubory ve složce `Moje dokumentace`, které už máte rozpracované, **nikdy nepřepisujte**. (Šablony nového modulu se rozbalí do nové složky, takže ke konfliktu nedojde.)

## 5. Šedé odkazy

Odkaz zobrazený šedě vede na modul, který ještě nebyl vydán. **Neklikejte na něj** — Obsidian by na jeho místě založil prázdnou poznámku, která by se později pletla se skutečným modulem. Pokud se to stane, prázdnou poznámku (případně i prázdnou složku) smažte.

## 6. Verze a opravy

- Každý soubor od učitele má nahoře řádek `> Verze: RRRR-MM-DD`.
- Co se kdy změnilo, najdete v [[CHANGELOG]].
- Při opravě dostanete ZIP modulu znovu — rozbalte ho podle bodu 4 a soubory od učitele přepište.

## 7. Nastavení Obsidianu

**Settings → Files and links → Default location for new attachments → *In subfolder under current folder*** a jako název podsložky zadejte `images`.

Screenshot pak stačí vložit do poznámky přes **Ctrl+V** a uloží se do `images` vedle ní — stejně jako u souborů od učitele.

## 8. Otisk a poctivost

Každý z vás staví **vlastní** infrastrukturu a vaše dokumentace to musí dokládat:

- **Vaše doména** `prijmeni.cyberschool.internal` (vaše příjmení bez diakritiky) — všude ve výstupech i na screenshotech.
- **Prompt PowerShellu s otiskem** — nastavíte ho v Modulu 0 na každém stroji. Vypadá takto:

  ```text
  [2026-10-08 09:41:12] NOVAK\Administrator@SRV1-DC PS C:\Users\Administrator>
  ```

  Každý textový výpis vkládejte **i s promptem**. Výstup bez promptu, s cizím účtem nebo s cizí doménou se nehodnotí.
- **Otisk stroje** (`…V0-O`) — výstup předepsaných příkazů. Obsahuje mimo jiné **UUID vašeho virtuálního stroje** a od Modulu 1 **SID vaší domény**; obojí je jedinečné pro každou instalaci a musí sedět se všemi ostatními výstupy.
- **Screenshoty s hodinami** — na každém screenshotu musí být vidět hodiny na hlavním panelu (datum a čas). Datum a čas musí odpovídat době, kdy jste pracovali.

Za **opis** se považuje zejména: shodné screenshoty nebo výpisy se spolužákem, cizí doména, UUID nebo SID, výstupy převzaté ze vzorového řešení nebo z příkladů v teorii (doména `novak`, ukázkové časy), upravované výstupy. Práce celé třídy se kontroluje najednou. Při podezření na opis následuje ústní ověření.

## 9. Odevzdání

1. Zabalte **jen** složku `Moje dokumentace\<Modul …>` (i s podsložkou `images`) do ZIPu.
2. ZIP pojmenujte `Prijmeni_Jmeno_ModulX.zip` — bez diakritiky, např. `Novak_Jan_Modul1.zip`.
3. Odevzdejte ho do příslušného **zadání v Teams**.

Modul 0 se dělá postupně na třech strojích (SRV1-DC před Modulem 1, PC1-WIN před Modulem 2, SRV2-FS před Modulem 6). Po přípravě každého stroje doplňte jeho část v `Moje dokumentace\Modul 0 Příprava` a složku Modulu 0 odevzdejte znovu — spolu s modulem, který na stroj navazuje.

## 10. Hodnocení

- Každá kolonka **postupu** a **důkazu** = **1 bod**:
  - **1** — úplné a správné,
  - **0,5** — neúplné nebo s drobnou chybou,
  - **0** — nevyplněné (`DOPLNIT`), špatně, nebo důkaz neodpovídá tomu, co má dokládat.
- Výsledek = získané body / maximum, v **procentech**.
- Uznává se i jiný správný postup se stejným výsledkem (GUI i PowerShell, jiný příkaz).
- Textový výstup bez promptu = 0 bodů. Screenshot bez viditelných hodin = nejvýš 0,5 bodu.

## 11. Když něco nefunguje

| Problém | Řešení |
|---|---|
| Smazali nebo přepsali jste soubor od učitele | Rozbalte znovu ZIP daného modulu. |
| Přišli jste o vlastní práci | Obnovte ji z historie verzí OneDrivu (pravým na soubor → *Version history*). |
| Klikli jste na šedý odkaz a vznikla prázdná poznámka | Smažte ji (bod 5). |
| Screenshot se uložil jinam než do `images` | Zkontrolujte nastavení z bodu 7 a soubor přesuňte. |
| Odkazy nebo obrázky nefungují | Vault musí být otevřený jako celá složka (bod 2), ne jednotlivé soubory. |
