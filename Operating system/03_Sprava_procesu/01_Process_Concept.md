---
aliases: [Process Concept, Pojem procesu]
---

# Pojem procesu

Staré počítače spouštěly vždy jen jeden program s plnou kontrolou nad systémem. Dnešní systémy nahrávají do paměti a spouští víc programů zároveň – to vyžaduje pevnější kontrolu a oddělení jednotlivých programů. Vznikl pojem **[[proces]]** = program v běhu, základní jednotka práce moderního časově sdíleného systému.

Systém se skládá ze **systémových procesů** (kód OS) a **uživatelských procesů** (kód uživatele) – všechny mohou běžet zdánlivě souběžně, protože se CPU mezi nimi přepíná.

## Základní pojmy

- **nejmenší jednotka pro adresování je bajt** – každý bajt v paměti má vlastní adresu
- **FIFO** (First In, First Out) – první dovnitř, první ven = **[[fronta]]** (queue)
- **LIFO** (Last In, First Out) – poslední dovnitř, první ven = **[[zásobník]]** (stack)
- **kompilátor (překladač)** – program, který přeloží **zdrojový kód** (psaný člověkem, např. v C) do **strojového kódu**, kterému rozumí procesor; výsledkem je spustitelný soubor (program), z něhož se po spuštění stane proces

## Struktura procesu v paměti

Proces je víc než jen program (ten se nazývá **text section** – jen pasivní soubor instrukcí na disku, tzv. spustitelný soubor). Proces je **aktivní entita**:

| Sekce                            | Obsah                                                               |     |
| :------------------------------- | :------------------------------------------------------------------ | --- |
| **Text section**                 | vlastní kód programu (sdílený, jen ke čtení)                        |     |
| **[[registr\|Program Counter]]** | adresa další instrukce k vykonání                                   |     |
| **[[zásobník\|Process Stack]]**  | dočasná data – parametry funkcí, návratové adresy, lokální proměnné |     |
| **Data section**                 | uložení všech proměnných                                            |     |
| **Heap**                         | odkazy na další části procesu v paměti                              |     |
| **Stack**                        | zásobník                                                            |     |

![[10ac508e4797d0d19e60645e174f249c591d85a2712ad0ebd88383b4058e8b59.png]]

Program se stane procesem, když se spustitelný soubor nahraje do paměti (dvojklikem na ikonu, nebo zadáním jména v příkazové řádce).

**Důležité:** dva procesy mohou pocházet ze stejného programu (např. víc kopií webového prohlížeče) – jde ale o dvě samostatné běžící instance. Text section mají stejný, ale data, heap a stack se liší.

### Proces jako běhové prostředí pro jiný kód

Proces může sám sloužit jako prostředí pro spuštění dalšího kódu – typický příklad je **Java Virtual Machine (JVM)**. JVM běží jako obyčejný proces, který interpretuje nahraný Java bajtkód a provádí akce (přes nativní instrukce) jeho jménem.

## Stavy procesu

Proces během svého běhu mění stav:

| Stav           | Popis                                                    |
| :------------- | :------------------------------------------------------- |
| **New**        | čerstvě načtený proces do paměti(když kliknu na soubor)  |
| **Ready**      | čeká, až mu bude přidělen procesor (ready queue)         |
| **Running**    | proces, který má přidělený procesor                      |
| **Waiting**    | čeká na nějakou událost (dokončení I/O, přijetí signálu) |
| **Terminated** | běh skončil                                              |

Názvy stavů se liší systém od systému, ale samotné stavy se vyskytují všude (některé OS je dělí ještě jemněji). **V daném okamžiku může na jednom procesoru běžet jen jeden proces** – ale procesů ve stavu Ready nebo Waiting může být víc najednou.

![[0765120d736644748f06cb0b43dce9b05f7ce4846e0db78857d927da644c4ef8.png]]

### Přechody mezi stavy

| Přechod | Z → do | Význam |
| :-- | :-- | :-- |
| **admitted** | New → Ready | proces je vytvořen a zařazen do **ready queue** |
| **ready queue** | Ready | **řada připravených procesů** – čekají na přidělení procesoru |
| **scheduler dispatch** | Ready → Running | **plánovač** ([[plánování procesů\|scheduler]]) vybere proces z ready queue a **dispatcher** mu přidělí procesor |
| **interrupt** | Running → Ready | **přerušení** (např. vyprší časové kvantum nebo přijde událost) – proces se vrátí do ready queue |
| **I/O or event wait** | Running → Waiting | proces čeká na dokončení I/O operace nebo na událost (např. čtení z disku) a procesor nepotřebuje |
| **I/O or event completion** | Waiting → Ready | čekání skončilo, proces se vrací do ready queue |
| **exit** | Running → Terminated | proces **skončil** úkol, nebo byl **ukončen (kill)** |

Z **Running** tedy proces jde buď do **Terminated** (hotovo / kill), do **Waiting** (čeká na I/O), nebo zpět do **Ready** (interrupt).

## Process Control Block (PCB)

Každý proces reprezentuje v operačním systému **PCB** (Process Control Block, taky Task Control Block) – datová struktura se všemi informacemi o daném procesu:

### Schéma PCB

![[pcb_schema.png|300]]

PCB je jakási **karta procesu** – operační systém si v ní drží vše potřebné, aby mohl proces kdykoli zastavit a později znovu spustit. Položky shora dolů:

| Položka                    | Co obsahuje                                                                            |
| :------------------------- | :------------------------------------------------------------------------------------- |
| **Process ID**             | jedinečné číslo procesu ([[PID]])                                                      |
| **State**                  | aktuální stav (new, ready, running, waiting, terminated)                               |
| **Pointer**                | ukazatel na další PCB (např. ve frontě připravených procesů) nebo na rodičovský proces |
| **Priority**               | priorita procesu pro plánovač                                                          |
| **Program counter**        | adresa další instrukce, která se má vykonat                                            |
| **CPU registers**          | uložené hodnoty registrů procesoru při přerušení                                       |
| **I/O information**        | informace o I/O                                                                        |
| **Accounting information** | spotřebovaný čas CPU, časové limity, čísla úloh (správce uloh)                         |
| **etc.**                   | další údaje (např. správa paměti)                                                      |

Při přepnutí CPU z jednoho procesu na jiný (**context switch**) se uloží PCB starého procesu a načte PCB nového – tím se obnoví přesně tam, kde proces skončil.

**CPU Switch from Process to Process (Contex switch)**

![[6c9fade4fee92377f108cb2f3ca3222d36175e575a2dc9e56a24d8e0da08025a.png]]

**Context switch** = přepnutí procesoru z jednoho procesu na druhý (na obrázku **P0** a **P1**, uprostřed jejich **PCB0** a **PCB1**).

1. **P0 běží** – procesor vykonává jeho instrukce
2. přijde **přerušení** nebo **systémové volání** (např. vyprší čas, nebo proces čeká na disk)
3. **uloží se stav P0 do PCB0** – program counter, registry, stav procesu
4. **načte se stav P1 z PCB1** – procesor dostane zpět registry a program counter procesu P1
5. **P1 běží**, P0 zatím čeká (idle)
6. později se to stane obráceně: uloží se PCB1, načte PCB0 a P0 pokračuje přesně tam, kde skončil

*Stručně: uložit PCB starého procesu, načíst PCB nového.*

**Pozor:** během přepnutí se nepočítá nic užitečného, systém jen ukládá a načítá → je to **režie**, proto se nechce přepínat zbytečně často.

## Vlákna (Threads)

Model popsaný výše předpokládá, že proces vykonává jen **jedno vlákno instrukcí najednou** (jedno vlákno řízení = může dělat jen jednu věc – např. nemůže psát text a zároveň kontrolovat pravopis v rámci jednoho procesu). Většina moderních OS ale umožňuje procesu mít **víc vláken (threads)** a dělat tak víc věcí najednou – výhodné hlavně na vícejádrových systémech, kde vlákna běží skutečně paralelně.

U systémů podporujících vlákna se PCB rozšiřuje o informace pro **každé vlákno zvlášť**.

![[3c8ca1f9558e193bfa957004af203bfb507bc6bf595dd03ee744ac5c5b73e65e.jpg]]

## Reprezentace procesu v Linuxu

![[aab99856603b139593c8b43b1cb1f002496809c5a0f1a27b65bb5725115895df.PNG]]

**Souvisí:** [[proces]], [[registr]], [[zásobník]], [[přerušení]], [[plánování procesů]]
