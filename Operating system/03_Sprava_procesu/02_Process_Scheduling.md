---
aliases: [Process Scheduling, Plánování procesů podrobně]
---
 
# Plánování procesů (podrobně)

Cíl **multiprogramování** – mít vždy nějaký proces běžící, maximalizovat využití CPU. Cíl **sdílení času (time sharing)** – přepínat procesor mezi procesy tak často, aby s nimi uživatel mohl interaktivně pracovat. **[[plánování procesů|Plánovač procesů]]** vybírá dostupný proces pro spuštění na CPU. Na jednoprocesorovém systému běží vždy nejvýš jeden proces, ostatní čekají.

## Plánovací fronty

- **Job queue** – všechny procesy v systému
- **Ready queue** – připravené a čekající na spuštění (obvykle jako [[spojový seznam]] – hlavička fronty ukazuje na první a poslední [[PCB]])
- **Device queue** – fronta procesů čekajících na konkrétní I/O zařízení (každé zařízení má vlastní frontu)

![[ca5ac492116f812ecf62ce379603b06045dac1b3fd4e0f24a1f91b860cbf1ecf.png]]


![[9a644713a05fe2a094c1ae13071c42b080e16a277bc3d3a2eff98b4c4614a188.png]]

## Plánovače (Schedulers)

Proces během své existence prochází různými plánovacími frontami – vybírá ho příslušný plánovač.

### Long-term scheduler (Job scheduler)

- Vyrábí nové procesy
- Volá se **zřídka** (sekundy až minuty) – může si dovolit být pomalejší
- **Spouští procesy** (**do new**)

### Short-term scheduler (CPU scheduler)

- Vybírá, který proces se spustí na CPU jako další
- Volá se **velmi často** (desítky až stovky milisekund) – musí být rychlý
- **Řadí procesy v ready queque**

Kdyby výběr trval 10 ms a proces pak běžel 100 ms, plánování by "zabralo" 10/(100+10) ≈ 9 % výkonu CPU zbytečně.

### Medium-term scheduler

Dívá se do paměti. Dočasně odebere proces z paměti (a tím i z boje o CPU), uloží ho na disk a později vrátí zpátky, kde skončil – tomuto mechanismu se říká **swapping**. Používá se ke zlepšení směsi procesů, nebo když dojde paměť.

![[28d8392ddb64e0a910f1af4d5aea6e2e254f0646fbbe9ed37e7904c942e20d4d.png]]

## CPU-bound vs. I/O-bound procesy

- **I/O-bound proces** – vytěžuje procesor, tráví víc času čekáním na vyřízení I/O než počítáním poté se přepne na CPU bound (prací na procesoru)
- **CPU-bound proces** – vytěžuje procesor, tráví víc času počítáním (prací na procesoru)

Dává CPu bound a I/O bound hnde za sebe a to řídí medium-term-sheduler

## Přepínání procesu(Context Switch)

Ukláda [[PCB]] stavy starého procesu (word) + načtení stavu nového (excel). Je to čistá režie ("pure overhead"). Typická rychlost je pár milisekund, což je pomalé oproti procesoru. Zabirá to čas procesoru přotože nic nedělá. Proto více kontex switchů nechcem.

**Dispatcher** - vyhazuje boudy pryč


![[6c9fade4fee92377f108cb2f3ca3222d36175e575a2dc9e56a24d8e0da08025a.png]]



**Souvisí:** [[proces]], [[PCB]], [[plánování procesů]], [[přerušení]], [[spojový seznam]]
