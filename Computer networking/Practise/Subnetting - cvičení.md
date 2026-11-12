# Subnetting – cvičení

Postup: [[Subnetting]]. Nejdřív počítej bez kalkulačky, řešení je dole.

## 1. Síť, broadcast, hosty

Pro `192.168.10.77/27` urči adresu sítě, broadcast a rozsah hostů.

## 2. Prefix ve 3. oktetu

Pro `172.16.45.200/21` urči adresu sítě, broadcast, masku a počet hostů.

## 3. Nejmenší prefix

Jaký nejmenší prefix potřebuješ pro 55, 120 a 500 hostů?

## 4. Dělení na podsítě

`192.168.5.0/24` rozděl na 6 stejných podsítí. Jaký bude prefix? Napiš první tři podsítě.

## 5. Velká síť

`10.0.0.0/8` rozděl na 1000 podsítí. Jaký bude prefix?

## 6. Stejná síť?

Jsou `192.168.1.130` a `192.168.1.190` ve stejné síti při masce `/26`?

## 7. Maska na prefix

Převeď `255.255.255.240` a `255.255.252.0` na lomítkovou notaci.

## 8. VLSM

Máš `192.168.50.0/24`. Potřebuješ: A = 100 hostů, B = 50, C = 25, D = 10 a dva spoje router–router (2 adresy). Přiděl podsítě od největší.

---

## Řešení

**1.** síť `192.168.10.64/27`, broadcast `192.168.10.95`, hosty `.65 – .94` (30)

**2.** blok 8 ve 3. oktetu: 45 → 40. Síť `172.16.40.0/21`, broadcast `172.16.47.255`, maska `255.255.248.0`, hostů 2046

**3.** 55 → `/26` (62), 120 → `/25` (126), 500 → `/23` (510)

**4.** 2³ = 8 ≥ 6 → `/27`. Podsítě `192.168.5.0/27`, `192.168.5.32/27`, `192.168.5.64/27`

**5.** 2^10 = 1024 ≥ 1000 → 8 + 10 = `/18`

**6.** Ano. Blok 64 → rozsah `.128 – .191`, obě adresy do něj spadají.

**7.** `/28` a `/22`

**8.**

| Podsíť | Hostů | Síť | Hosty | Broadcast |
| :-- | :-- | :-- | :-- | :-- |
| A | 100 | 192.168.50.0/25 | .1 – .126 | .127 |
| B | 50 | 192.168.50.128/26 | .129 – .190 | .191 |
| C | 25 | 192.168.50.192/27 | .193 – .222 | .223 |
| D | 10 | 192.168.50.224/28 | .225 – .238 | .239 |
| Spoj 1 | 2 | 192.168.50.240/30 | .241 – .242 | .243 |
| Spoj 2 | 2 | 192.168.50.244/30 | .245 – .246 | .247 |

Volné od `192.168.50.248`.
