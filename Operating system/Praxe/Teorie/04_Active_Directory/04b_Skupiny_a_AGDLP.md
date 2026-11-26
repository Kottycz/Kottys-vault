---
aliases: [Skupiny a AGDLP, Oprávnění přes skupiny]
tags: [ops, teorie]
---

# Skupiny a model AGDLP

Žáci mají mít přístup ke složce `Verejne`, informatici k vývojovým nástrojům, učitelé ke směrnicím a vedení k důvěrným dokumentům. Kdybychom oprávnění nastavovali každému člověku zvlášť, s každým novým žákem by přibyly desítky nastavení a při změně pravidel bychom je opravovali všude znovu. Proto se oprávnění **nedávají lidem, ale skupinám**: člověk dostane práva tím, že se stane členem skupiny, a ztratí je, když ji opustí. [[OU]] určují, **jak se objekty spravují**, skupiny určují, **k čemu mají přístup**.
Předchozí: [[04a_Navrh_OU]] · Další: [[04c_Ucty_a_pripojeni_PC]] · Pojem: [[AGDLP]]

> **Jako klíče od budovy:** místo vlastního klíče od každé místnosti pro každého učitele vydáš klíče „sborovna“, „kabinet informatiky“ a podle role přidělíš sadu klíčů.

---

## Pojmy

| Pojem | Význam |
| :-- | :-- |
| **skupina** | objekt v [[AD DS\|AD]], který sdružuje uživatele, počítače nebo jiné skupiny |
| **bezpečnostní skupina** (Security) | lze jí přidělit oprávnění → používáme |
| **distribuční skupina** (Distribution) | jen pro rozesílání pošty, oprávnění dát nejde |
| **rozsah** (scope) | kdo smí být členem a kde jde skupina použít: Global, Domain Local, Universal |
| **vnořování** (nesting) | skupina je členem jiné skupiny |
| **[[AGDLP]]** | Accounts → Global groups → Domain Local groups → Permissions |
| **[[ACL]]** | seznam oprávnění u souboru nebo složky (kdo smí co) |
| **`GG_` / `DL_`** | naše předpony: globální skupina / doménová lokální skupina |

## Typ a rozsah skupiny

Každá skupina má **typ** a **rozsah**.

**Typ:**

- **Security** – jde jí dát oprávnění (a jde použít i pro e-mail) → používáme vždy
- **Distribution** – jen e-mailový seznam

**Rozsah** určuje, kdo může být členem a kde se skupina použije:

| Rozsah | Kdo může být členem | Kde ji jde použít | K čemu ji používáme |
| :-- | :-- | :-- | :-- |
| **Global** | uživatelé a skupiny **ze stejné domény** | v celém lese | sdružení lidí **podle role** („všichni učitelé“) |
| **Domain Local** | členové z libovolné domény lesa | **jen ve vlastní doméně** | **konkrétní právo ke zdroji** („zápis do složky Vedeni“) |
| **Universal** | členové z libovolné domény lesa | v celém lese | prostředí s víc doménami; u nás s jednou doménou nepotřebujeme (navíc zatěžuje replikaci) |

**Zapamatuj si: Global = kdo je člen (role), Domain Local = k čemu má právo (zdroj).**

## Vnořování skupin

Skupina může být členem jiné skupiny. Využíváme to u souhrnných skupin:

- `GG_Zamestnanci` obsahuje `GG_Ucitele`, `GG_Vedeni` a `GG_THP`
- `GG_Studenti` obsahuje `GG_Studenti_G8`, `GG_Studenti_G4`, `GG_Studenti_EL` a `GG_Studenti_IT`

Pravidla:

- uživatel je **přímo** členem jen **nejmenší** skupiny (obor, role); do souhrnné se dostane **vnořením**
- nový žák informatiky → přidáš ho do `GG_Studenti_IT` a automaticky je i v `GG_Studenti`; když škola bude chtít něco jen pro informatiky, skupina už existuje
- žáky **nepřidáváme přímo** i do `GG_Studenti` – duplicitní členství se snadno rozejde
- podle rozsahu: Global může obsahovat jen Global ze stejné domény; Domain Local může obsahovat Global i Domain Local ze stejné domény
- vnořuj jen tak hluboko, aby šlo zjistit, **proč** má uživatel nějaké právo
- výpis členů i s vnořenými: `Get-ADGroupMember <skupina> -Recursive`

## Model AGDLP

[[AGDLP]] je osvědčený postup, jak oprávnění uspořádat:

1. **A**ccounts – uživatelské účty (`eva.student`)
2. **G**lobal groups – účty se zařadí do globálních skupin **podle role** (`GG_Studenti_IT`)
3. **D**omain **L**ocal groups – globální skupina se vloží do doménové lokální skupiny **navázané na zdroj** (`DL_Informatika_Zapis`)
4. **P**ermissions – oprávnění u zdroje (složka `Informatika`: Modify) dostane **jen ta doménová lokální skupina**

Výhody:

- **správa členství místo správy [[ACL]]** – změna, kdo smí do složky, je změna členství ve skupinách; oprávnění u složky se nemění
- **čitelnost** – z názvu `DL_Informatika_Zapis` je jasné, k čemu skupina je
- **opakované použití** – stejná globální skupina (`GG_Ucitele`) může být v mnoha DL skupinách pro mnoho složek
- **bezpečnost** – pár jednoznačných oprávnění se kontroluje snáz než desítky výjimek pro jednotlivce

**Zlaté pravidlo:** oprávnění u zdroje nastavuj **jen doménovým lokálním skupinám, nikdy jednotlivým lidem**.

Doménové lokální skupiny (`DL_…`) zakládáme až v **Modulu 6 a 7**, kde vznikají sdílené složky – vážou se totiž na konkrétní zdroj. V Modulu 4 zakládáme jen globální skupiny podle rolí.

### Příklad: složka předmětové komise

| Krok | Co | Příklad |
| :-- | :-- | :-- |
| 1 | uživatel je v globální skupině role | `jana.teacher` → `GG_PK_Informatika` |
| 2 | globální skupina je členem DL skupiny | `GG_PK_Informatika` → `DL_PK_Informatika_Zapis` |
| 3 | DL skupina má právo ke zdroji | `DL_PK_Informatika_Zapis` → `Predmetove-komise\Informatika`: Modify |
| 4 | přijde nový učitel informatiky | jen ho přidáš do `GG_PK_Informatika` a právo má |

Když se změní pravidlo (např. do složky `Vedeni` smí zapisovat i zástupce ředitele), přidáš zástupce do `GG_Vedeni` – u složky se nic nemění.

## Naše skupiny

V [[OU]] `Skola\Skupiny` je **14 bezpečnostních skupin s rozsahem Global**:

| Skupina | Členové | Proč existuje |
| :-- | :-- | :-- |
| `GG_Studenti` | vnořené `GG_Studenti_G8`, `_G4`, `_EL`, `_IT` | všichni žáci – společná oprávnění |
| `GG_Studenti_G8` / `_G4` / `_EL` / `_IT` | žáci oborů (gymnázium 8leté, 4leté, elektrotechnika, informatika) | pravidla a oprávnění podle oboru |
| `GG_Zamestnanci` | vnořené `GG_Ucitele`, `GG_THP`, `GG_Vedeni` | všichni zaměstnanci |
| `GG_Ucitele` | pedagogové | společná oprávnění učitelů |
| `GG_Vedeni` | ředitel, zástupci | složka vedení, jiná pravidla než ostatní |
| `GG_THP` | sekretariát, hospodářka (technicko-hospodářští pracovníci) | administrativa |
| `GG_Sekretariat` | kdo fyzicky sedí v sekretariátu | ukázka [[GPO]], která platí jen pro vybranou skupinu (Modul 5) |
| `GG_PK_Matematika`, `GG_PK_Informatika`, `GG_PK_Jazyky` | učitelé předmětových komisí | sdílená složka komise |
| `GG_IT-Sprava` | správci IT | budoucí delegování správy |

## U nás

- všech 14 globálních bezpečnostních skupin v [[OU]] `Skupiny`, vnořené `GG_Ucitele`, `GG_THP`, `GG_Vedeni` do `GG_Zamestnanci` a čtyři oborové do `GG_Studenti`
- uživatele přidáváme jen do **nejmenší** vhodné skupiny (žáka do oborové, učitele do `GG_Ucitele` a komise)
- `DL_` skupiny navázané na složky vzniknou v Modulu 6 a 7
- oprávnění ke složkám a tiskárnám dostávají jen skupiny
