---
aliases: [Duplicate Address Detection, detekce duplicitní adresy]
tags: [slovnik]
---

# DAD

**Duplicate Address Detection** – ověření, že [[IPv6]] adresa, kterou si chce zařízení vzít, není už použitá někým jiným.

---

## Podrobně

### Kdy proběhne

Vždy, než zařízení začne adresu používat – u [[LLA]], adresy ze [[SLAAC]] i staticky nastavené.

### Průběh

1. Adresa je ve stavu **tentative** (zkušební) – nelze ji zatím používat
2. Zařízení pošle [[NS]] na tuhle adresu: „má někdo 2001:db8::100?"
3. Vyhodnocení odpovědi:
   - **nikdo neodpoví** (po pár vteřinách) → adresa je volná → přejde do stavu *preferred* a používá se
   - **někdo odpoví [[NA]]** → adresa je obsazená → nelze ji použít. U SLAAC se vygeneruje jiná, u statické se nahlásí chyba

### Proč je to potřeba

V IPv6 si zařízení adresu často **vytváří samo** ([[SLAAC]]) – nikdo centrálně neeviduje, kdo co má. DAD je pojistka, že nevznikne konflikt.

### Rozdíl oproti IPv4

V IPv4 je to volitelné (některé systémy dělají „gratuitous [[ARP]]"), v IPv6 je DAD **povinná součást** [[NDP]] a proběhne vždy.

### Co když DAD selže

Zařízení adresu nepoužije. U link-local adresy odvozené z [[MAC adresa|MAC]] to znamená, že IPv6 na tom rozhraní vůbec nenaběhne – většinou jde o duplicitní MAC adresu (typicky chyba ve virtualizaci).

**Souvisí:** [[NDP]], [[NS]], [[NA]], [[SLAAC]], [[IPv6]], [[LLA]], [[ARP]]
