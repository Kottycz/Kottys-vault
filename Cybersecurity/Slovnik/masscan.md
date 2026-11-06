---
aliases: [masscan]
tags: [slovnik]
---

# masscan

Velmi rychlý skener portů a hostitelů, určený pro **obrovské rozsahy adres**.

*Příklad: projít celou podsíť /16 (asi 65 tisíc adres) za krátkou dobu.*

---

## Podrobně

- v místnosti se zmiňuje spolu s [[arp-scan]] jako nástroj, který se částečně překrývá s [[nmap|Nmapem]]
- Nmap je přesnější a bohatší na funkce, masscan je hlavně **rychlý**
- rychlost znamená víc síťového provozu → víc šumu
- syntaxe: `-p` + port / seznam / rozsah, např. `masscan MACHINE_IP/24 -p80,443`, `-p22-25`, `--top-ports 100`
- instalace: `apt install masscan` (v AttackBoxu není předinstalovaný)

**Souvisí:** [[nmap]], [[arp-scan]], [[zjišťování živých hostitelů]]
