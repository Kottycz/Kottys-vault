# Základní pojmy a paradigmata počítačových sítí

## Přenos vs. zpracování

**Přenos** – „to, co se přenáší, se nemění". Mohou se přenášet jednotlivé bity/byty, nebo celé bloky dat.

**Zpracování** – „to, co se zpracovává, se nepřenáší". Vzdálenost není podstatná.

## Směr přenosu

- **Simplexní** – umožňuje přenos jen v jednom směru (např. klasické TV a rozhlasové vysílání). „Kanál je vždy simplexní."
- **(Plně) duplexní** – umožňuje přenos v obou směrech současně. [[full-duplex|Plně duplexní]] okruh = lze komunikovat oběma směry zároveň.
- **[[half-duplex|Poloduplexní]]** – umožňuje přenos v obou směrech, ale ne současně.

## Kanál, okruh, cesta, spoj

„To, co přenáší."

**Uzel** – „to, co má smysl propojovat":
- servery
- (hostitelské) počítače
- terminály
- periferie (tiskárny, plottery, externí disky…)
- mobily, PDA…

## Proudový přenos

- Přenášená data nejsou nijak členěna, tvoří „souvislý proud" (stream) na úrovni bitů, bytů, slov…
- Představa: přenosová cesta se chová jako roura – z jedné strany se do ní data vkládají, z druhé ve stejném pořadí vystupují.
- Vhodné tam, kde je 1 odesílatel a 1 příjemce – přenos „bod-bod". Odesílatelem je „ten, kdo vkládá", příjemcem „ten, kdo vyjímá".

## Blokový přenos

- Data jsou pro potřeby přenosu členěna na vhodně velké celky – **bloky**.
- Bloky mohou (ale nemusí) být opatřeny údaji, které identifikují odesílatele a příjemce.

## Přepojování paketů

Obecný princip, jak přenášet data na bázi sdílené přenosové kapacity.

Podstata:
- Žádná přenosová kapacita se nevyhrazuje, zůstává společná.
- Odesílatel předá data k doručení – musí být členěna na bloky (pakety) a opatřena identifikací příjemce. Proudový přenos zde nemá smysl.
- K přenosu se přijímají bloky od všech odesílatelů, manipuluje se vždy s celými bloky (odsud „přepojování paketů").
- Rozhoduje se podle identifikace příjemce, kterou si každý blok nese ve své hlavičce.
- K přenosu jednotlivých paketů se vždy využívá celá dostupná přenosová kapacita – pro všechny odesílatele i příjemce. Proto musí být pakety označeny identifikací odesílatele a příjemce.

## Spojovaný přenos

- Funguje **stavově** – komunikující strany přechází mezi různými stavy. Např. výpadek spojení je třeba nejprve detekovat, pak zrušit spojení a navázat nové.
- Přenášené bloky dat obsahují ve své hlavičce **identifikátor spojení** a jsou přenášeny podle tohoto ID.
- Zachovává **pořadí** – při postupném přenosu jsou všechny bloky přenášeny stejnou cestou, proto se jejich pořadí nemůže měnit.

Příklad: [[TCP]].

## Nespojovaný přenos

- Funguje **bezestavově** – komunikující strany nepřechází mezi různými stavy, jejich stav se v průběhu komunikace nemění.
- Nemusí být explicitně ošetřovány změny stavů a nestandardní situace – jednoduše se pokračuje dál.
- Terminologie: bloky dat přenášené nespojovaným způsobem se často označují jako **datagramy**.

Příklad: [[UDP]].

## CISCO Academy – hostitelské role

Termín **hostitelé** se vztahuje na zařízení v síti, kterým je pro komunikační účely přiřazeno číslo identifikující je v rámci konkrétní sítě – **[[IP adresa]]**. IP adresa identifikuje hostitele i síť, ke které je připojen.

Příklad klientského softwaru: webový prohlížeč (Chrome, Firefox).
