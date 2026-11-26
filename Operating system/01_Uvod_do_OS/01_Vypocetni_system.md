# Výpočetní systém

Výpočetní systém má čtyři části:

- **Hardware** – základní výpočetní zdroje ([[CPU]], paměť, V/V zařízení)
- **[[operační systém]]** – řídí a koordinuje využití hardwaru mezi aplikacemi a uživateli
- **Aplikační programy** – určují, jak se zdroje použijí (editory, kompilátory, prohlížeče, hry…)
- **Uživatelé** – lidé, stroje, jiné počítače

## CPU (procesor)

- **srdce** výpočetního systému – načítá a vykonává instrukce z paměti, počítá matematické a logické operace, řídí tok dat
- moderní mikroprocesor = všechny části v jednom integrovaném obvodu
- pracuje binárně, čísla se ale obvykle zapisují šestnáctkově (viz [[Ciselne_soustavy]])
- řídí ho **systémové hodiny** – každý impuls = operace; frekvence (např. 100 MHz) ale sama neurčuje výkon, různé procesory stihnou za impuls různě práce

### CPU registry

**[[registr|Registry]]** = interní paměť procesoru pro data; velikost a počet závisí na procesoru (Intel 32bit, Alpha 64bit).

Speciální registry:

- **Program Counter (PC)** – adresa další instrukce, po načtení se sám zvýší
- **Stack Pointer (SP)** – vrchol zásobníku (LIFO)
- **Processor Status (PS)** – stav procesoru včetně režimu (jádro / uživatel)

## Sběrnice (BUS)

Propojuje obvody na základní desce:

- **adresová** – adresa v paměti pro přenos
- **datová** – obousměrná, přenos dat mezi CPU a pamětí
- **řídící** – časovací a řídicí signály

Pro periferie: ISA, PCI.

## Paměť

Hierarchie od nejrychlejší:

- **[[cache]]** – nejrychlejší a drahá, dočasná kopie hlavní paměti (malá v procesoru, větší na desce)
- **[[RAM]]** – rychlá pracovní paměť během výpočtu
- **[[ROM]]** – jen pro čtení, neměnné programy (bootstrap)
- **[[EEPROM]]** – přepisovatelná, ale ne často (firmware)
- **vnější paměť** – disky, flash, cloud – trvalé uložení

- **volatilní** – bez napájení ztratí obsah (RAM)
- **nevolatilní** – obsah zůstane ([[ROM]], [[HDD]], [[SSD]], NVRAM)

**Sekundární úložiště** – hlavní paměť je malá a volatilní, proto [[HDD]] (nejběžnější) a [[SSD]] (rychlejší).

## Řadiče (Controller)

- **[[řadič|Řadiče]]** ovládají periferie (grafika, disky) – jsou to vlastně „pomocné procesory“ s vlastními registry
- CPU potřebuje pro každý řadič **ovladač zařízení**, který s registry pracuje
- **[[DMA]]** – velké přenosy (zápis na disk) jdou přímo do paměti bez zatěžování CPU po celou dobu přenosu

## Start systému

**[[bootstrap]] program** ve [[firmware|firmwaru]] (ROM/EEPROM) po zapnutí:

1. inicializuje systém (registry CPU, řadiče, paměť)
2. najde jádro OS a nahraje ho do paměti
3. předá mu řízení

Po nahrání **[[kernel|jádra]]** se spustí **systémové procesy / démoni** (UNIX: první je `init`) a systém čeká na událost.

## Přerušení (Interrupt)

- událost signalizuje **[[přerušení]]** – od hardwaru (signál po sběrnici) nebo softwaru (systémové volání)
- CPU přeruší práci a skočí na obslužnou rutinu
- rychlost zajišťuje **vektor přerušení** – tabulka adres rutin indexovaná číslem zařízení

## RTC (Real Time Clock)

- přesný čas a pravidelné intervaly
- vlastní baterie → PC zná čas i po vypnutí

## Von Neumannova architektura

Většina systémů má jeden univerzální procesor. **Multiprocesorové systémy** (paralelní, těsně vázané):

- vyšší propustnost, úspora z rozsahu, vyšší spolehlivost
- **ASMP** (asymetrický) – každý procesor má svůj úkol
- **SMP** (symetrický) – každý proces může běžet na kterémkoli procesoru

## Vstup/výstup (I/O)

- velká část kódu OS je správa V/V; každý řadič má **ovladač** s jednotným rozhraním
- **interrupt-driven I/O** – řadič po přenosu ohlásí konec přerušením
- velké objemy (disky) přes **[[DMA]]** → jedno přerušení na celý blok, ne na každý bajt
