---
aliases: [Process Synchronisation, proces synchronizace, Synchronizace procesů]
---

# Synchronizace procesů

Když víc procesů (vláken) přistupuje ke stejnému prostředku (paměť, soubor, V/V), musí zůstat v **konzistentním stavu** – dokud jeden zapisuje, jiný nesmí zapisovat ani číst, jinak dostane napůl změněná data. Řeší to **algoritmy synchronizace procesů**.

## Bernsteinovy podmínky

1. nesmí se **číst**, když jiný proces **zapisuje**
2. nesmí se **zapisovat**, když jiný proces **zapisuje**

![[e78819a1039e6458065db6eaa58858272e4bebf40c8eed09fbdadaa19b89c9ca.png]]

## Kritická sekce

**Kritická sekce** = nejmenší část kódu, která přistupuje ke sdílenému prostředku a nesmí v ní být víc procesů najednou. Vstup hlídá **synchronizační primitivum** (výhradní přístup, konečné čekání).

![[e130a0d5363d0ab2ff5b9098901e9a63e78a7a3e9e8853e67cc11dc557c9acc1.png]]

**Tři podmínky přístupu:**

- **výhradní přístup** – uvnitř nejvýš jeden proces
- **rozhodování o vstupu** – rozhodují jen procesy, které chtějí dovnitř
- **omezené čekání** – rozhodnutí se nesmí odkládat donekonečna (viz [[starvation]])

Čekající procesy můžou **aktivně čekat** – pořád zkoušet vstoupit.

## Synchronizační primitiva

### Zámek a instrukce TSL (Test and Set Lock)

- procesorová instrukce (má ji většina procesorů): nastaví `Lock` na „zamčeno“ a vrátí předchozí hodnotu
- použije se v čekací smyčce (aktivní čekání):

```
while TestAndSet(Lock) do { nothing };
   ...kód kritické sekce...
Lock := false;
```

- musí být **atomická** (proběhne celá, nebo vůbec), jinak nechrání

![[0fbd0f0b2e0e6f1ebdc7ee510e7ff643c2e057e19d324edd3d7d2a3a4e7cfac9.png]]

**Instrukce TSL (Test and Set Lock)**

![[c8584099ef535bd5a7cd7a0222ce246b13a5abc7eca6010080d7f4d57d4889a9.png]]

![[c9d42b7c0cd59f5535790021678c2373210ea2c67421a54b740ac3357ef1b39c.png]]

### Semafor

![[88795e5c4f0f5d3499a8d09a0498cb78acf8b2102ada361ce8cc32b25c76db83.png]]

**Binární semafor:**
- **0 (červená)** – `wait()` proces zablokuje a zařadí do fronty; `release()` probudí prvního čekajícího (nebo nastaví 1)
- **1 (zelená)** – `wait()` pustí proces dovnitř a nastaví 0

**Obecný semafor** – čítač:
- **záporný** = počet čekajících procesů
- **0** = prostředek se používá
- **kladný** = tolikrát se dá projít bez čekání
- `Wait()` −1 (pod 0 → zablokuje), `Signal()` +1 (≤ 0 → odblokuje prvního čekajícího)

![[185947207c032fef1630304bd097ca08b0b3fb9475ee831fa965824d18bbd76b.png]]

### Mutex (Mutual Exclusion)

Brání souběhu dvou kritických kódů nad stejným prostředkem. Stavy **volný** / **vlastněný** (drží ho konkrétní [[PID|proces]] + počet uzamknutí).

![[c1307ad12cab99fed82dbd6fcdeb2cdf827a2eb43b6de743c193b5c1d7fba170.png]]

- **lock** – volný → proces je vlastník (1); vlastní ho už on → +1; vlastní jiný → čeká
- **unlock** – vlastník → −1, při 0 se uvolní pro čekající
- **riziko:** špatné použití → zpomalení nebo **[[uváznutí|deadlock]]**

## Klasické synchronizační úlohy

### Producent–konzument

Producent dává položky do fronty omezené velikosti, konzument je odebírá. Konzument čeká při prázdné frontě, producent při plné.

**Producent**

![[7333a9fa20d60461d9bea31bee05bf06381aa90ce085e2ccf473ec2e78f3fb33.png]]

**Konzument**

![[561d08d86126ceb10f8c451a2cbd73725fdd2859f412167b41333bbfcc516635.png]]

**Řešení dvěma semafory:**
- **semafor 1** = volná místa (na začátku velikost fronty) – snižuje producent
- **semafor 2** = zaplněná místa (na začátku 0) – snižuje konzument

### Čtenáři–písaři

**Čtenáři** jen čtou (můžou současně), **písaři** zapisují – ==zápis musí být exkluzivní==.

- **priorita čtenářů** → hrozí **starvation** písařů
- **priorita písařů** → hrozí starvation čtenářů

### Hodující filozofové

n filozofů u kulatého stolu, mezi každými dvěma jedna hůlka, k jídlu potřebují dvě.

- všichni zvednou pravou hůlku → nikdo nemá levou → **uváznutí**
- řešení:
  - **jedna židle navíc** – ke stolu jen n−1 filozofů
  - **číšník** – rozhoduje, kdo si smí vzít hůlky
  - **hierarchie zdrojů** – hůlky očíslované, bere se vždy nejdřív nižší → žádné cyklické čekání

![[e055500a6c80404cc3311c2371839b41c59303fd665bcbfad520e400b7ad93dd.png]]

## Synchronizační rizika

### Uváznutí (Deadlock)

- procesy se zablokují křížovým čekáním – každý čeká na to, co drží ten druhý
- řeší se preventivně (návrh algoritmu) nebo zásahem (ukončení procesu, rollback)
- příklad: A drží tiskárnu a chce pásku, B drží pásku a chce tiskárnu

![[1dd01ff6741df2be19f7220d05b2476a82c1f1961bd3849dce32ee6d9360e1f6.png]]

### Livelock

- procesy **aktivně** zkouší pokračovat, ale pořád selhávají – nejsou zablokované, ale nepostoupí
- filozofové zvednou levou hůlku, nikdo nemá pravou, všichni položí a zkusí znovu – donekonečna

![[e055500a6c80404cc3311c2371839b41c59303fd665bcbfad520e400b7ad93dd.png]]

### Starvation (vyhladovění)

- proces čeká na prostředky donekonečna, protože pořád přichází procesy s vyšší prioritou
- např. plánování disku SSTF odsouvá požadavky daleko od hlavy

![[b574ad230e5e7d45c4c2f5d45c0f341901bfd416ece1c77a89e9b1630f962661.jpg]]

### Souběh (Race Condition)

- víc procesů pracuje se stejnými daty a [[přepnutí kontextu]] uprostřed operace pokazí výsledek; kdyby běžely po sobě, chyba by nevznikla
- příklady: souběžný vklad a výběr z účtu, dva procesy vytváří soubor stejného jména

![[bad1f2d3317f026675f2692c3c9e527478a8a81aeee8c08977d687472db9b55a.png]]

**Současně provedený vklad a výběr peněz**

![[96b2dae1c3f285e77e214af16492cb2505992ad1cb79f54b012d20d2dd7e2dd2.png]]

**Současné vytváření souboru stejného jména dvěma procesy**

![[ff1e5579fa85e51e1bfb99b4150cbb92aad6b744de272b5b0e7a6af289018ea0.png]]

**Souvisí:** [[proces]], [[vlákno]], [[uváznutí]], [[starvation]], [[přepnutí kontextu]], [[IPC]]
