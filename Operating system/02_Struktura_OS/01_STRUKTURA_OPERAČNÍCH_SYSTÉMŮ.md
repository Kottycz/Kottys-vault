---
aliases: [Struktura operačních systémů, Struktura OS, Architektura OS, Architektury jader]
tags: [os]
---

# ARCHITEKTURA OS

> Přepis xmind mapy **01_STRUKTURA_OPERAČNÍCH_SYSTÉMŮ** (Teams) – stejná struktura jako v mapě, zkrácené do odrážek.

## STRUKTURA OS

U moderních OS je struktura navržená hlavně s ohledem na ==bezpečnost a stabilitu== celého systému.

### Hardwarová ochrana prostředků

- procesor umí vykonávat kód na **několika úrovních oprávnění** – každá určuje, které instrukce a operace jsou povolené
- na x86 jsou to ==čtyři okruhy (RING 0 až RING 3)==; ==čím nižší číslo, tím víc smí==
- okruh procesu určuje, jak smí přistupovat k chráněným prostředkům (paměť, I/O, některé instrukce procesoru)
- **Ring 0** – vše: přímá komunikace s hardwarem, řízení procesoru, tabulka vektorů přerušení, tabulka segmentů
- **Ring 1 a 2** – některé instrukce už zakázané; využívají je některé virtualizace (servery)
- **Ring 3** – nesmí nic, co by ovlivnilo OS, ani přímo komunikovat s hardwarem
- většina OS (i Windows) používá jen **2 okruhy**: **RING 0** pro jádro a ovladače, **RING 3** pro aplikace

![[Pasted image 20261001123504.png]]

### Režimy běhu procesů

Běh procesů se vždy dělí na dva režimy:

- **privilegovaný režim** (režim jádra, kernel mode) – běží **jádro** OS = Ring 0
- **uživatelský režim** (user mode) – běží **aplikace** = Ring 3; nemůžou nijak zasahovat do privilegované části

![[Pasted image 20261001123532.png|245]]

**Poznámka z hodiny (OPS)**

> [!abstract] Operační systém
> Co potřebujeme:
>
> - ==správce CPU== – `ring 0`
> - ==správce paměti== – `ring 0`
> - ==správce I/O== – `ring 0`
> - ==grafické rozhraní== **GUI** nebo **CLI** – stačí `ring 3`
> - ==souborový systém==

> [!tip] Ring 0 a Ring 3
> - Programy v `ring 0` říkáme ==kernel==
> - **Ring 0** = ==jádro==
> - **Ring 3** = ==aplikace==

### A jak to spolu souvisí

- **procesor** je hlavní nástroj OS – používá ho pro vlastní výpočty a dává ho k dispozici aplikacím
- jeho mechanismy (úrovně oprávnění) OS využívá k ochraně hardwaru před zákeřnými programy a k ochraně kódu jádra před změnami

![[Pasted image 20261001123708.png]]

### VYUŽITÍ RING 1 PŘI VIRTUALIZACI

- na hardware se nainstaluje vrstva ==HYPERVISOR== a teprve nad ni operační systémy
- **hypervisor** = rozhraní mezi hardwarem a hostovanými OS
  - k hardwaru: správa a optimální vytěžování (load balancing)
  - k OS: abstrakce hardwaru – každý OS má iluzi, že běží sám na své konfiguraci

![[Pasted image 20261001123623.png]]

#### PRINCIP VIRTUALIZACE

![[Pasted image 20261001123739.png]]

### ZÁKLADNÍ TYPY ARCHITEKTUR

Používají se pro systém jako celek i pro jeho části (jádro, vrstvy v jádře, ovladače, služby).

![[Pasted image 20261001123754.png]]

#### MONOLITICKÁ

- **nejjednodušší** struktura: **jádro** + **rozhraní** ke komunikaci s okolím
- jádro je obvykle **jeden soubor** (Linux: `/boot/vmlinuz`)
- funkce se za běhu rozšiřují **moduly** (knihovny, např. DLL)
- monolitické jsou jádra **UNIXU** a **WINDOWS NT** (i když mají přesnou vnitřní strukturu)

##### MS DOS

![[Pasted image 20261001124053.png]]

##### TRADIČNÍ UNIX

![[Pasted image 20261001124146.png]]

#### MICROKERNEL

- velmi **malé jádro** – jen **virtuální paměť, plánování vláken, obsluha výjimek, komunikace mezi procesy**
- ostatní (souborové systémy, síť, správce procesů a paměti, I/O) běží v **uživatelském režimu** jako aplikace
- **výhody:** ==vyšší stabilita==, menší nároky na vývojáře
  - pád jedné součásti neshodí celý systém (ovladač nemůže přepsat data jádra)
  - často stačí komponentu restartovat
  - méně kritického kódu

![[fba5ffd0d5c60f803acd8e23d938bd2bf80316df154a54c4cecd7c175f9a31b2.png]]

##### MACH

![[8e1bf37924d04cb1b6a6c1dc6dd37914895c040c5bdc60848bcd6ad84cacf8df.jpg]]

##### HURD

![[2376707942dad8c18d26f0f01b09dfb853a353c58f4e34e3a99afeee2a3871a2.png]]

- https://www.gnu.org/software/hurd/

##### OS X

![[6df8bc3fc3c2887ebd6feedff10dc94ac4f39e96f591ae68bd0f07b870b3dc95.gif]]

###### OS X DETAILNĚJI

![[61ba59654d93358a6531fe3b580abbfb28b277790157378d29b77d9c88758e44.svg]]

#### VRSTVENÁ/HIERARCHICKÁ

- části systému jsou ve **vrstvách**; každá využívá jen služeb **nižší** vrstvy a mluví jen se sousedními
- staví se zevnitř ven → vnitřní (nejdůležitější) vrstvy jsou nejlépe otestované
- známe ze sítí (ISO/OSI, TCP/IP); u OS takhle vypadá systém jako celek: ==VRSTVA JÁDRA== a ==UŽIVATELSKÁ VRSTVA==

![[336722f12d976223721595688249346fd0f2af494c432b115dcdd4d1e5495403.png]]

#### MODULÁRNÍ

- jádro dává **základní služby** (procesy, paměť, výjimky, přerušení), zbytek se nahrává ==dynamicky== při startu nebo při prvním použití
- tak se načítají souborové systémy, ovladače, síťové protokoly – bez překompilování jádra
- potřebuje přesně definované jednotné rozhraní modulů (i pro moduly, které vznikly po jádru)
- **výhoda oproti mikrokernelu:** moduly jsou **součástí jádra** → komunikují přímo, ne přes zprávy
- používají **SOLARIS, LINUX, MAC OS X, WINDOWS**

![[96f61bd631f92fe473edb29c022d26110cb020b283705683042f4dedcc8c79ab.png]]

#### HYBRIDNÍ

V praxi skoro žádný OS nemá jednu čistou strukturu – **kombinují se přístupy** kvůli výkonu, bezpečnosti a použitelnosti.

- **LINUX** a **Solaris** – monolitické (jeden adresový prostor, výkon) a zároveň modulární
- **Windows** – hlavně monolitické (výkon), ale s prvky mikrokernelu (podsystémy v uživatelském režimu) a s dynamickými moduly jádra

![[434b903d4fae000fff60782340b6ae74476742f793cd8725985c423b068559ae.png]]

##### WINDOWS S NT JÁDREM

![[3f54fb54a230b50c1ee0b6af61be5ce8119b2bd950701c9e440d138494f8a9c6.png]]

##### GNU/LINUX

![[a60c2df2756acd3c915c9b76efcb81261fdcb21224856c6cb650f051a0689565.png]]

#### POROVNÁNÍ MONOLITIC-MICROKERNEL-HYBRID

![[2dd4f64029e8f74bf190689014312e626596b3eebcf64e8806fd67a60d14e9f4.png]]

## ZDROJE

- http://www.vmware.com/download/player/
- https://www.osboxes.org/vmware-images/
- http://www.vmware.com/appliances/

---

**Struktura OS:** [[01_STRUKTURA_OPERAČNÍCH_SYSTÉMŮ|Architektury OS]] · [[01a_Windows|Windows]] · [[01b_Unix|UNIX]] · [[01c_Linux|Linux]] · [[01d_Apple|Apple]] · [[01e_Android|Android]]
