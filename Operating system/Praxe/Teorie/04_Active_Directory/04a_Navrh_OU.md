---
aliases: [Návrh struktury OU, Organizační jednotky]
tags: [ops, teorie]
---

# Návrh struktury OU

Doména z Modulu 1 je prázdná. Kdyby se do ní uživatelé a počítače zakládali bez rozmyslu, vznikl by jeden dlouhý seznam, ve kterém nepoznáš, kdo je žák, kdo učitel a který počítač stojí v učebně. Přitom na každou z těch skupin budeme chtít **jiná pravidla** (Modul 5), **jiná oprávnění** (Modul 6–7) a třeba i **jiného správce**. Tahle poznámka řeší, jak strukturu domény navrhnout.
Další: [[04b_Skupiny_a_AGDLP]] · [[04c_Ucty_a_pripojeni_PC]] · Základy: [[01a_Domena_a_AD]]

> **Jako složky v počítači:** soubory řadíš podle toho, co s nimi budeš dělat, ne podle toho, kdo je vytvořil. U [[OU]] stejně – objekty řadíme podle toho, **jak je budeme spravovat**.

---

## Pojmy

| Pojem | Význam |
| :-- | :-- |
| **[[OU]]** (organizační jednotka) | kontejner v doméně pro uživatele, skupiny a počítače; může obsahovat další [[OU]] |
| **kontejner** | výchozí „složka“ (`Users`, `Computers`, `Builtin`); nejde na ni navázat [[GPO]] |
| **[[GPO]]** | soubor nastavení, který se aplikuje na objekty v [[OU]] (Modul 5) |
| **delegování správy** | svěření vybraných úkonů (např. reset hesla) jinému uživateli jen pro určitou [[OU]] |
| **[[DN]]** | úplná cesta k objektu, např. `CN=Eva Svobodová,OU=Informatika,OU=Studenti,OU=Skola,DC=kotrba,DC=cyberschool,DC=internal` |
| **ochrana proti smazání** | příznak [[OU]], který brání jejímu náhodnému smazání |
| **Advanced Features** | zobrazení v [[ADUC]] (View → Advanced Features), které odkryje další záložky (např. *Object*) |

## K čemu je OU

[[OU]] má v doméně **tři úlohy**:

1. **třídění** – v [[ADUC]] hned vidíš, kdo kam patří
2. **navázání [[GPO]]** – zásada navázaná na [[OU]] platí pro všechny objekty uvnitř (i ve vnořených [[OU]]) → žáky omezíš jinak než učitele
3. **delegování správy** – správu jedné [[OU]] (třeba reset hesel žáků) může dostat někdo jiný než správce celé domény, např. učitel informatiky

**[[OU]] není skupina:**

- do [[OU]] se objekty **zařazují** – objekt je vždy **jen v jedné [[OU]]**
- do skupin se uživatelé **přidávají** – můžou být v **mnoha skupinách**
- [[OU]] slouží ke **správě** ([[GPO]], delegace), skupiny k **oprávnění** (viz [[04b_Skupiny_a_AGDLP]])

## Kontejner × OU

Po vytvoření domény v ní jsou výchozí objekty:

| Výchozí | K čemu | Pozn. |
| :-- | :-- | :-- |
| `Users` | výchozí místo pro nové uživatele a skupiny (i vestavěný `Administrator`) | kontejner → **[[GPO]] nejde** |
| `Computers` | výchozí místo pro počítače po připojení do domény | kontejner → počítače proto přesouváme do [[OU]] |
| `Builtin` | vestavěné lokální skupiny domény (Administrators, Backup Operators…) | neměníme |
| `Domain Controllers` | řadiče domény | je to **[[OU]]** se speciálními [[GPO]]; neměníme ji a nic do ní nepřesouváme |

→ proto zakládáme vlastní kořenovou [[OU]] **`Skola`**: naše objekty jsou oddělené od výchozích a můžeme na ně cíleně navazovat zásady.

## Podle čeho OU dělit

Častá chyba je zkopírovat do domény **organizační schéma** (ředitel, zástupci, vedoucí oddělení). Schéma se ale mění při každé reorganizaci, a přitom se nemění, jaká pravidla na lidi platí. Lepší je dělit podle **způsobu správy**. Novou [[OU]] má smysl založit, když:

- na objekty mají platit **jiná pravidla** (jiné [[GPO]]) – např. žáci × učitelé
- je bude spravovat **někdo jiný** (delegace)
- jde o **jiný typ objektu** – uživatelé, počítače, skupiny a servisní účty se nemíchají

[[OU]] naopak nedělíme tam, kde by se jen složitě udržovala:

- žáky **nedělíme po ročnících** – ročník se každý rok mění a museli bychom žáky stále přesouvat
- dělíme je **po oborech** – obory se liší výukou, učebnami i potřebným softwarem
- strom drž **mělký** (pár úrovní) – hluboká struktura se špatně spravuje a hůř se předpovídá, které zásady kde platí

## Naše struktura

```text
kotrba.cyberschool.internal
└── Skola
    ├── Zamestnanci
    │   ├── Ucitele
    │   ├── Vedeni
    │   └── THP            (technicko-hospodářští pracovníci)
    ├── Studenti
    │   ├── Gymnazium-8lete
    │   ├── Gymnazium-4lete
    │   ├── Elektrotechnika
    │   └── Informatika
    ├── Pocitace
    │   ├── Servery
    │   ├── Klienti-Ucebny
    │   └── Klienti-Kancelare
    ├── Skupiny
    └── Sluzebni-ucty
```

| [[OU]] | Co v ní je | Proč samostatně |
| :-- | :-- | :-- |
| `Zamestnanci` | učitelé, vedení, THP | jiná pravidla než žáci |
| `Studenti` (po oborech) | žáci čtyř oborů | různé obory mají různé potřeby |
| `Pocitace` | servery, klienti v učebnách a kancelářích | servery mají jiná pravidla než klienti, učebny jiná než kabinety |
| `Skupiny` | bezpečnostní skupiny | aby se nepletly mezi uživatele a počítače |
| `Sluzebni-ucty` | účty pro služby (zálohování, plánované úlohy) | jiná pravidla hesel, nikdo se na ně nepřihlašuje jako uživatel |

- názvy **bez diakritiky a mezer** (`Zamestnanci`, `Klienti-Ucebny`) – snadnější práce v PowerShellu a hledání v logách, vždy stejný zápis; slova oddělujeme pomlčkou
- `PC1-WIN` patří do `Pocitace\Klienti-Ucebny`; na tuhle strukturu se v Modulu 5 navážou [[GPO]]

## Ochrana proti smazání

- při zakládání [[OU]] je ve výchozím stavu zaškrtnuté **Protect container from accidental deletion** → [[OU]] nejde smazat jedním kliknutím
- když ji opravdu chceš smazat: [[ADUC]] → **View → Advanced Features** → vlastnosti [[OU]] → záložka **Object** → odškrtnout ochranu
- necháváme ji zapnutou u všech [[OU]] – smazání celé [[OU]] i s obsahem je jedna z nejnepříjemnějších chyb správce

## Delegování správy

- pravým na [[OU]] → **Delegate Control…** → průvodce: vybereš skupinu a úkon (např. *Reset user passwords and force password change at next logon*)
- skupina pak smí ten úkon dělat **jen v dané [[OU]]**
- v projektu ho nepoužíváme (všechno dělá `Administrator`), ale struktura s ním počítá – správu `Studenti\Informatika` by šlo svěřit učiteli informatiky

## U nás

- kořenová [[OU]] `Skola` a pod ní strom výše
- `Domain Controllers` necháváme beze změny
- žáci podle oboru, zaměstnanci podle role, `PC1-WIN` do `Pocitace\Klienti-Ucebny`
- skupiny a servisní účty ve vlastních [[OU]]
- na strukturu navážou v Modulu 5 zásady skupiny
