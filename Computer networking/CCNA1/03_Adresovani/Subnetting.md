# Subnetting

Dělení sítě na menší podsítě půjčováním bitů z hostitelské části. Základ viz [[IPv4_adresovani]], [[maska podsítě]], [[délka prefixu]]. Cvičení: [[Subnetting - cvičení]].

## Postup: do které sítě patří adresa

1. **Host bity** = 32 − prefix
2. **Velikost bloku** = 2^(host bity); v „zajímavém" oktetu = 256 − hodnota masky
3. **Adresa sítě** = nejbližší násobek bloku, který je ≤ adrese
4. **Broadcast** = adresa další sítě − 1
5. **Hosty** = síť + 1 až broadcast − 1

Příklad `192.168.1.100/26`:

```
/26 → maska .192 → blok 256 − 192 = 64
násobky 64: 0, 64, 128, 192 → 100 patří do 64
síť 192.168.1.64 · broadcast 192.168.1.127 · hosty .65 – .126
```

## Postup: kolik hostů / podsítí potřebuju

- **Hosty:** nejmenší `h`, pro které 2^h − 2 ≥ potřeba → prefix = 32 − h
- **Podsítě:** nejmenší `n`, pro které 2^n ≥ počet podsítí → nový prefix = starý + n

Příklad: `192.168.5.0/24` na 6 podsítí → 2³ = 8 ≥ 6 → půjčit 3 bity → `/27` (blok 32).

## Rychlé hodnoty

| Prefix | Maska (poslední oktet) | Blok | Hosty |
| :-- | :-- | :-- | :-- |
| /25 | .128 | 128 | 126 |
| /26 | .192 | 64 | 62 |
| /27 | .224 | 32 | 30 |
| /28 | .240 | 16 | 14 |
| /29 | .248 | 8 | 6 |
| /30 | .252 | 4 | 2 |

Pro prefixy v 3. oktetu stejný princip: /21 → maska `255.255.248.0` → blok 8 ve 3. oktetu.

## Časté chyby

- zapomenuté −2 (adresa sítě a [[broadcast]])
- blok se hledá v **oktetu, kde maska končí**, ne vždy v posledním
- [[VLSM]]: vždy od největší podsítě, jinak se bloky nezarovnají

**Souvisí:** [[VLSM]], [[maska podsítě]], [[délka prefixu]], [[IPv4_adresovani]]
