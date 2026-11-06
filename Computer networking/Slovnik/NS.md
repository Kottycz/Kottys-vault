---
aliases: [Neighbor Solicitation]
tags: [slovnik]
---

# NS

**Neighbor Solicitation** – zpráva [[NDP]], kterou se zařízení ptá na [[MAC adresa|MAC adresu]] souseda. Obdoba ARP Requestu v [[IPv6]]. Odpovědí je **NA** (Neighbor Advertisement).

---

## Podrobně

### Tři použití

| Situace | Co se ptá |
| :-- | :-- |
| **Překlad adresy** | "kdo má tuhle IPv6 adresu? Pošli MAC." (jako [[ARP]]) |
| **[[DAD]]** | "má už někdo tuhle adresu?" – ptá se na *vlastní* adresu, než ji použije |
| **Kontrola dostupnosti** | "jsi ještě tam?" – ověření, že soused funguje |

### Průběh (překlad adresy)

```
PC1 chce poslat data na 2001:db8::9, nezná jeho MAC.

NS →  solicited-node multicast (ff02::1:ff00:9)
      "kdo má 2001:db8::9?"

NA ←  unicast zpátky PC1
      "já, moje MAC je 00:1A:2B:3C:4D:5E"

PC1 si dvojici uloží do neighbor cache.
```

### Solicited-node multicast

NS nejde [[broadcast|broadcastem]] jako ARP, ale na speciální [[multicast]] adresu odvozenou z posledních 24 bitů hledané adresy:

```
ff02::1:ff  +  posledních 24 bitů cílové adresy
```

Zprávu tak zpracuje jen hrstka zařízení se shodným koncem adresy, ne celá síť. To je efektivnější než ARP.

### Neighbor cache

Naučené dvojice IPv6 ↔ MAC se ukládají do **neighbor cache** (obdoba ARP tabulky):

- Linux: `ip -6 neigh`
- Windows: `netsh interface ipv6 show neighbors`

**Souvisí:** [[NDP]], [[ARP]], [[DAD]], [[IPv6]], [[MAC adresa]], [[multicast]]
