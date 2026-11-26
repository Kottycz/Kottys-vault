---
aliases: [Čas, jazyk a soukromí, Kerberos a čas]
tags: [ops, teorie]
---

# Čas, jazyk a soukromí

Vypadá to jako vedlejší nastavení, ale dopad je velký: **špatný čas** = uživatel se nepřihlásí do domény, i když zná heslo; **špatný formát data** = logy nejdou rozumně číst ani řadit; **zbytečná telemetrie** = data o stroji a lidech odcházejí ven; **chybějící prompt s otiskem** = nepoznáš, kdy a kde byl příkaz spuštěn. Proto se to řeší hned na začátku.
Praxe: [[00_Priprava_OS]] · Předchozí: [[00b_Identita_a_sit]]

> **Jako hodinky v orchestru:** když každý hraje podle jiných hodin, orchestr se rozpadne, i když všichni umí hrát.

---

## Čas

### UTC a časové pásmo

- počítač si čas pamatuje ve **[[UTC]]** (světový čas) a podle **časového pásma** ho zobrazuje jako místní
- Česko: `(UTC+01:00) Praha, Bratislava, Budapešť, Lublaň` = *Central Europe Standard Time*; v létě [[UTC]]+2, přechod řídí systém sám, když je pásmo správně

Co se stane, když je pásmo špatně:

- logy a události mají časy v jiné hodině → hůř se dohledává, co se kdy stalo
- plánované úlohy běží ve špatný čas
- někdo „opraví“ hodiny ručně – na displeji to sedí, ale **uvnitř je špatné [[UTC]]** → problémy s Kerberem

### NTP a Windows Time

- hodiny v počítači se časem rozjíždějí → musí se **synchronizovat** s časovým serverem přes **[[NTP]]**
- ve Windows to dělá služba **Windows Time (W32Time)**
- v doméně platí **hierarchie**:
  - **řadič domény** (konkrétně držitel role [[FSMO|PDC]] emulator, viz [[FSMO]]) bere čas z přesného zdroje na internetu
  - **ostatní servery a klienti** berou čas z řadiče
- výsledek: všechny stroje v doméně mají stejný čas mezi sebou, i kdyby byl zdroj o vteřinu jinde

### Kerberos a 5 minut

**[[Kerberos]]** je protokol, kterým se v doméně přihlašuje.

- při přihlášení klient posílá **časové razítko**, server ho porovná se svým časem
- rozdíl hodin se jmenuje **clock skew**; když je větší než **5 minut** (výchozí tolerance [[AD DS|AD]]), žádost se zamítne
- důvod: ochrana proti **replay útoku** – útočník, který zachytí starou žádost, ji nemůže za chvíli použít znovu, protože je „prošlá“
- důsledek: s rozjetými hodinami se uživatel **nepřihlásí ani se správným heslem**; hlásí se to jako *přístup odepřen*, ale problém je v hodinách
- samotné špatné **pásmo** Kerberos nerozbije (porovnává se [[UTC]]) – rozbije ho až ruční přehození hodin kvůli špatnému pásmu

## Jazyk, region a klávesnice

Ve Windows jsou to **tři nezávislá nastavení**, která se často pletou:

| Nastavení | Co určuje | Naše hodnota |
| :-- | :-- | :-- |
| **jazyk rozhraní** (display language) | jazyk menu, oken, hlášek | English (United States) |
| **formát regionu** (region format) | datum, čas, čísla, měna | Czech (Czech Republic) |
| **klávesnice** (input method) | jaké znaky dávají klávesy | US + Czech (QWERTZ), výchozí US |
| **home location** | země pro funkce podle polohy | Czech Republic |
| **formát data / času** | zobrazení v systému | `d.M.yyyy` a `H:mm:ss` |

Proč zrovna takhle:

- **anglické rozhraní** – konzole, chybové hlášky i dokumentace Microsoftu jsou anglicky; kdo zná anglické názvy, snáz najde řešení a složí certifikaci
- **české formáty** – datum, čísla a měna tak, jak je čteme; tak je to i v českých firmách
- **dvě klávesnice** – na US se snadno píšou znaky do příkazů (`\`, `|`, `{ }`), CZ je na diakritiku; přepínání `Win + mezerník`

Pro dokumentaci a logy je důležitý zápis `2026-10-08 09:41:12` (rok-měsíc-den, 24 h): dá se seřadit podle abecedy i času a nedá se splést (je `3. 4.` třetí duben, nebo čtvrtý březen?). Proto ho používá prompt.

## Soukromí a telemetrie

Windows posílá Microsoftu **diagnostická data** (telemetrii) – informace o stroji, výkonu, chybách a případně o používání aplikací. Má dvě úrovně:

| Úroveň | Obsah |
| :-- | :-- |
| **Required** (povinná) | minimum, aby systém fungoval a byl aktualizovaný |
| **Optional** (volitelná) | podrobnosti o používání a chybách |

Na školních strojích pracují žáci a učitelé → chceme, aby ven odcházelo **co nejméně dat**:

| Nastavení | Hodnota | Proč |
| :-- | :-- | :-- |
| diagnostická data | Required | minimum |
| Inking & typing | vypnuto | text, který píšeš, nemá odcházet |
| Tailored experiences | vypnuto | nabídky podle tvých dat |
| poloha | vypnuto | škola polohu stroje nepotřebuje |
| reklamní ID | vypnuto | reklamní sledování |
| Find My Device (jen PC1) | vypnuto | hledání přes Microsoft účet |

Teď se to dělá ručně, aby bylo vidět, kde nastavení je; později (Modul 5) to půjde centrálně přes [[GPO]] pro celou školu.

## Prompt s otiskem

Na všech strojích má PowerShell prompt, který před každým příkazem ukáže **datum, čas, účet a počítač**:

```text
[2026-10-08 09:41:12] SRV1-DC\Administrator@SRV1-DC PS C:\Users\Administrator>
```

- každý výpis v dokumentaci tak **sám dokazuje, kdo, kde a kdy** ho pořídil
- při hledání chyby víš, na kterém stroji a v kolik se co stalo
- při hodnocení je to důkaz, že výstup je z tvého prostředí → **výstupy bez promptu se nehodnotí**
- prompt je v **profilu PowerShellu** (skript, který se spustí při startu konzole) pro všechny uživatele (`AllUsersAllHosts`), aby fungoval i doménovým účtům
- aby se profil načetl, musí být povolené spouštění skriptů – zásada `RemoteSigned` (Windows 11 má výchozí `Restricted`, profil by se nespustil); nastavuje se pro **celý počítač**

## U nás

- pásmo **Praha**, čas z internetu, v doméně z řadiče
- rozhraní English (US), formáty Czech, klávesnice US + CZ, home location Czech Republic
- telemetrie na minimu, poloha a reklamní ID vypnuté
- prompt s otiskem na všech strojích
