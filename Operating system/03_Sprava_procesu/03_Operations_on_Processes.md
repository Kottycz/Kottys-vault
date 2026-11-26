---
aliases: [Operations on Processes, Operace s procesy]
---

# Operace s procesy – vytváření a ukončování

Procesy běží souběžně a dynamicky vznikají a zanikají → systém musí umět **vytvářet a ukončovat procesy**.

## Strom procesů

- proces, který vytvoří jiný, je **rodič (parent)**, nový je **potomek (child)**; každý má jedinečné **PID**
- v Linuxu je kořenem **`init`** (vždy PID 1) – vznikne po startu a vytváří další procesy; každý proces se dá vysledovat až k němu
- výpis: `ps -el`

![[1247f8e65fda453310b12fa724ac14372b8b7f937a7e9268922e66add2d09bba.png]]

## Vytváření procesu (Process Creation)

Potomek potřebuje zdroje (CPU, paměť, soubory, V/V). Rodič může:

- nechat ho získat zdroje přímo od OS
- omezit ho na část svých zdrojů (ochrana proti zahlcení systému)
- sdílet s ním některé zdroje
- předat mu vstupní data

![[2436974c030ceb350802b6c6dd7f1e365027758209630b95e88e2511d685d373.png]]

- **běh:** rodič běží **souběžně** s potomkem, nebo **čeká**, až potomek skončí
- **adresový prostor:** potomek je **kopie** rodiče, nebo se do něj nahraje **nový program**

![[e72a19cfc36668ed8bd42c7669e77b04f5782321ff6eabe93121fc1fb7d287ba.png]]

## Vytváření procesů v Linuxu/UNIXu

- **`fork()`** – nový proces jako **kopie adresového prostoru** rodiče; oba pokračují za `fork()`, liší se návratovou hodnotou: potomek **0**, rodič **PID potomka**
- **`exec()`** – **přepíše** paměť procesu novým programem; vrací se jen při chybě
- **`wait()`** – rodič čeká, dokud potomek neskončí (nebo běží souběžně a nevolá ho)
- potomek dědí **oprávnění, plánovací atributy a některé zdroje** (otevřené soubory); `exec()` volat nemusí a může dál běžet jako kopie

![[87093d266fe4b22f4ccf5975b9debcce196da1e068b712f3a50f85415aaf580b.png]]

**C program – příklad**

![[cd6b85a8eea15ad08166d849d3d1674db556b05995585f6214aea389b9c7933e.png]]

## Vytváření procesů ve Windows

- **`CreateProcess()`** – na rozdíl od `fork()` **rovnou nahraje zadaný program** (nekopíruje rodiče) a má aspoň 10 parametrů
- parametry: **`STARTUPINFO`** (okno, standardní vstup/výstup) a **`PROCESS_INFORMATION`** (handle a ID procesu a vlákna)
- místo `wait()` je **`WaitForSingleObject()`**

![[8f2b524e574f970303b4550f3de5c3c029c19a4e9e2f76ee2f769ab332fe830c.png]]

## Ukončení procesu (Process Termination)

- proces po poslední instrukci zavolá **`exit()`** a vrátí stav rodiči (přes `wait()`)
- OS uvolní všechny jeho zdroje (paměť, soubory, buffery)

![[ec8dd7fea72500460d0fe99717398016695a8f05ed52e38bc646e61a111b8ad2.png]]

### Násilné ukončení

- systémovým voláním (Windows `TerminateProcess()`); obvykle smí jen **rodič** → musí znát své potomky
- důvody: potomek překročil limit zdrojů, jeho úkol už není potřeba, rodič končí

### Kaskádové ukončení (Cascading Termination)

Na některých systémech když skončí rodič, **musí skončit i všichni potomci** – zařídí to OS.

![[76fdc475c55a98cc5828f5c9a57179830a94c5a603bd450cf5c58e0b95cdebc3.png]]

### Zombie a orphan procesy

- **zombie** – proces skončil, ale rodič ještě nezavolal `wait()` → záznam v tabulce procesů zůstává, dokud ho rodič nevyzvedne; krátce tím projde každý proces
- **orphan** – rodič skončil dřív, než zavolal `wait()` → v Linuxu ho adoptuje **`init`**, který pravidelně volá `wait()`

**wait() system call**

![[4771210454e921d9af1984792a852de1db23027f4b46246bf35d9ec0e2ce874f.png]]

**Zombie & Orphan**

![[598e27e4fec6f4167c83137a64df8227cc6b7f6c7cd7b81c1b4086e70ab12372.png]]

**Souvisí:** [[proces]], [[PCB]], [[systémové volání]], [[přerušení]]
