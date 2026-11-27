---
aliases: [Open Shortest Path First]
tags: [slovnik]
---

# OSPF

**Open Shortest Path First** – dynamický směrovací protokol. [[router|Routery]] si mezi sebou vyměňují informace o síti a každý si sám spočítá nejkratší cestu ke všem cílům.

---

## Podrobně

### Statické vs. dynamické směrování

- **statické** – cesty zadává admin ručně (`ip route`), při výpadku linky se samy nezmění,
- **dynamické** – routery si cesty zjistí samy a při výpadku si najdou jinou. OSPF je dynamický protokol typu **link-state**.

### Jak funguje

1. Routery si najdou **sousedy** (Hello zprávy na [[multicast]] `224.0.0.5`)
2. Vymění si **LSA** (Link State Advertisements) – popis svých spojů a jejich cen
3. Každý router si z nich sestaví **stejnou mapu celé sítě** (link-state database, LSDB)
4. Pomocí **Dijkstrova algoritmu (SPF)** si spočítá nejkratší cestu ke každé síti
5. Nejlepší cesty zapíše do [[směrovací tabulka|směrovací tabulky]]

Když spoj spadne, router to hned pošle sousedům v LSA, všichni si přepočítají cesty.

### Hello a Dead časovač

- **Hello interval** – jak často router posílá Hello (na Ethernetu **10 s**),
- **Dead interval** – za jak dlouho bez Hello prohlásí souseda za mrtvého (výchozí **40 s**, tj. 4× Hello).

Aby se dva routery staly sousedy, musí mít **stejné** Hello a Dead časovače, stejnou oblast (area) a být ve stejné podsíti. Nesoulad je častá chyba v labech.

### Stavy sousedství

`Down → Init → 2-Way → ExStart → Exchange → Loading → Full`

- **2-Way** – vidí se navzájem v Hello,
- **Full** – mají synchronizovanou databázi, sousedství je hotové. Tohle chceš vidět v `show ip ospf neighbor`.

### DR a BDR

Na sítích s více routery na jednom segmentu (Ethernet) by si každý vyměňoval LSA s každým. Proto se zvolí:

- **DR** (Designated Router) – ostatní posílají aktualizace jen jemu (multicast `224.0.0.6`), on je rozešle,
- **BDR** (Backup DR) – záloha, převezme roli, když DR spadne.

Volí se podle **priority rozhraní** (vyšší vyhrává), při shodě podle vyššího **Router ID**.

### Router ID

Jednoznačná identifikace routeru v OSPF, zapisuje se jako IPv4 adresa. Určí se v tomto pořadí:

1. ručně příkazem `router-id`,
2. nejvyšší IP na [[loopback]] rozhraní,
3. nejvyšší IP na aktivním fyzickém rozhraní.

### Metrika – cost

Cena spoje se odvozuje od **šířky pásma** (rychlejší linka = nižší cena). Protokol tedy preferuje rychlé cesty, ne nejmenší počet [[hop|hopů]]. Cena cesty = součet cen všech linek po cestě.

```
cost = referenční šířka pásma / šířka pásma linky
výchozí reference = 100 Mb/s
```

| Linka | Cost |
| :-- | :-- |
| 10 Mb/s Ethernet | 10 |
| 100 Mb/s FastEthernet | 1 |
| 1 Gb/s GigabitEthernet | 1 |

Problém: s výchozí referencí mají 100 Mb/s i 1 Gb/s stejný cost 1. Proto se na všech routerech zvyšuje reference: `auto-cost reference-bandwidth 1000`.

### Administrativní vzdálenost

Když router zná cestu do stejné sítě z víc zdrojů, vybere tu s nižší **AD**. OSPF má AD **110** (statická cesta 1, EIGRP 90, RIP 120). V `show ip route` jsou OSPF cesty označené písmenem **O**.

### Oblasti (areas)

Ve velkých sítích se OSPF dělí na **oblasti**, aby routery nemusely počítat celou síť:

- **Area 0 (backbone)** – páteřní oblast, všechny ostatní se na ni napojují
- Ostatní oblasti komunikují mezi sebou jen přes Area 0
- malé sítě (a CCNA laby) používají **single-area OSPF**, tj. jen Area 0

### Základní konfigurace

```
R1(config)# router ospf 10
R1(config-router)# router-id 1.1.1.1
R1(config-router)# network 192.168.10.0 0.0.0.255 area 0
R1(config-router)# network 10.0.0.0 0.0.0.3 area 0
R1(config-router)# passive-interface g0/0/1
```

- `10` je **process ID**, platí jen lokálně, sousedé ho mít stejný nemusí,
- za sítí se píše **wildcard maska** (obrácená maska: `/24` → `0.0.0.255`),
- `passive-interface` – na rozhraní do LAN se neposílají Hello, ale síť se dál inzeruje.

### Ověření

| Příkaz | Co ukáže |
| :-- | :-- |
| `show ip ospf neighbor` | sousedy a jejich stav (Full) |
| `show ip route ospf` | cesty naučené přes OSPF |
| `show ip protocols` | Router ID, sítě, AD |
| `show ip ospf interface brief` | rozhraní v OSPF, cost, role DR/BDR |

### Typy směrovacích protokolů

| Typ | Princip | Příklady |
| :-- | :-- | :-- |
| **Distance vector** | „soused mi řekl, jak daleko to je" | RIP, [[EIGRP]] |
| **Link state** | „znám mapu celé sítě, počítám sám" | **OSPF**, IS-IS |
| **Path vector** | cesty mezi autonomními systémy | [[BGP]] |

### Vlastnosti

- **Otevřený standard** (na rozdíl od Cisco [[EIGRP]]) – funguje napříč výrobci
- **Classless** – posílá i [[maska podsítě|masku]], podporuje [[VLSM]]
- **Rychlá konvergence** – na výpadek reaguje během vteřin
- **Aktualizace jen při změně**, ne celé tabulky pořád dokola jako RIP
- **OSPFv2** pro [[IPv4]], **OSPFv3** pro [[IPv6]]

**Souvisí:** [[router]], [[směrovací tabulka]], [[VLSM]], [[multicast]], [[IP adresa]], [[maska podsítě]], [[EIGRP]], [[BGP]], [[loopback]]
