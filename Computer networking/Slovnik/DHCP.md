---
aliases: [Dynamic Host Configuration Protocol, DHCPv4, DHCPv6]
tags: [slovnik]
---

# DHCP

**Dynamic Host Configuration Protocol** – automaticky přiděluje zařízením [[IP adresa|IP adresu]] a další síťové nastavení. Běží nad [[UDP]], server na portu **67**, klient na **68**.

---

## Podrobně

### Co řeší

Bez DHCP by se musela každému počítači ručně nastavit IP adresa, [[maska podsítě]], [[default gateway]] a [[DNS]] server. V síti o stovkách zařízení je to nereálné – DHCP to udělá automaticky.

### Co všechno přiděluje

- **IP adresu** (z definovaného rozsahu = pool)
- **[[maska podsítě|Masku podsítě]]**
- **[[default gateway|Výchozí bránu]]**
- **[[DNS]] servery**
- případně další (doménu, NTP server…)

### Proces DORA

Přidělení adresy probíhá ve čtyřech krocích (viz [[DORA]]):

1. **DISCOVER** – klient se ptá [[broadcast|broadcastem]]: „je tu DHCP server?"
2. **OFFER** – server nabídne konkrétní adresu
3. **REQUEST** – klient si ji vyžádá
4. **ACK** – server přidělení potvrdí

Klient zpočátku nemá žádnou adresu, proto se ptá broadcastem (na `255.255.255.255`).

### Zapůjčení (lease)

Adresa se nepřiděluje natrvalo, ale **na dobu zapůjčení** (lease time, např. 24 h). Klient si ji v polovině doby automaticky obnovuje (REQUEST → ACK). Když se odpojí a lease vyprší, adresa se vrátí do poolu pro jiné zařízení.

### Statická vs. dynamická adresa

- **Dynamická** – přiděluje DHCP, může se změnit. Vhodné pro běžné počítače, mobily.
- **Statická (rezervace)** – DHCP přidělí vždy stejnou adresu podle [[MAC adresa|MAC adresy]]. Vhodné pro servery, tiskárny, [[router|routery]].

### DHCP pro IPv6

U [[IPv6]] existuje **DHCPv6**, ale často se místo něj používá [[SLAAC]] – zařízení si adresu vytvoří samo podle informací z [[RA]].

**Souvisí:** [[DORA]], [[IP adresa]], [[maska podsítě]], [[default gateway]], [[broadcast]], [[SLAAC]], [[UDP]]
