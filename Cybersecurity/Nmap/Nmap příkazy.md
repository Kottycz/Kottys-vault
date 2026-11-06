# Nmap – přehled příkazů

Tahák ze zápisu [[01_Nmap_Live_Host_Discovery|Nmap – Live Host Discovery]]. `MACHINE_IP` = IP cíle.

## Určení cílů

| Co | Příklad |
| :-- | :-- |
| seznam | `nmap 10.11.12.15 10.11.12.20` |
| rozsah | `nmap 10.11.12.15-20` |
| podsíť | `nmap MACHINE_IP/30` |
| cíle ze souboru (`-iL`) | `nmap -iL seznam.txt` |
| jen vypsat cíle, neskenovat (`-sL`) | `nmap -sL 10.10.68.220/24` |

## Zjišťování živých hostitelů

| Metoda | Příkaz | Poznámka |
| :-- | :-- | :-- |
| [[ping scan]] | `nmap -sn MACHINE_IP/24` | jen zjistí živé hostitele, neskenuje porty |
| [[ARP]] | `sudo nmap -PR -sn MACHINE_IP/24` | jen stejná podsíť |
| [[ICMP]] echo ([[ping]]) | `sudo nmap -PE -sn MACHINE_IP/24` | typ 8 → 0 |
| [[ICMP timestamp]] | `sudo nmap -PP -sn MACHINE_IP/24` | typ 13 → 14, když je echo blokováno |
| [[ICMP address mask]] | `sudo nmap -PM -sn MACHINE_IP/24` | typ 17 → 18, často blokováno |
| [[TCP SYN ping]] | `sudo nmap -PS22,80,443 -sn MACHINE_IP/30` | [[TCP]], výchozí port 80, viz [[3-way handshake]] |
| [[TCP ACK ping]] | `sudo nmap -PA22,80,443 -sn MACHINE_IP/30` | [[TCP]] s příznakem [[ACK]], vyžaduje privilegovaného uživatele |
| [[UDP ping]] | `sudo nmap -PU53,161,162 -sn MACHINE_IP/30` | [[UDP]], čeká [[ICMP]] „port nedostupný" |

- porty za `-PS` / `-PA` / `-PU`: číslo (`-PS21`), rozsah (`-PS21-25`), seznam (`-PS80,443,8080`)
- bez `-sn` Nmap po zjištění hostitelů **skenuje jejich porty**

## DNS

| Volba | Význam |
| :-- | :-- |
| `-n` | žádné [[DNS]] dotazy |
| `-R` | [[reverzní DNS]] pro všechny hostitele, i offline |
| `--dns-servers DNS_SERVER` | použít konkrétní DNS server |

## arp-scan

| Příkaz | Význam |
| :-- | :-- |
| `sudo arp-scan -l` | skenuje všechna rozhraní (místní sítě) |
| `sudo arp-scan -I eth0 -l` | jen rozhraní `eth0` |
| `sudo arp-scan --localnet` | místní síť (alternativa k `-l`) |
| `sudo apt install arp-scan` | instalace |

Viz [[arp-scan]].

## masscan

| Příkaz | Význam |
| :-- | :-- |
| `masscan MACHINE_IP/24 -p443` | port 443 |
| `masscan MACHINE_IP/24 -p80,443` | seznam portů |
| `masscan MACHINE_IP/24 -p22-25` | rozsah portů |
| `masscan MACHINE_IP/24 --top-ports 100` | 100 nejčastějších portů |
| `apt install masscan` | instalace |

Viz [[masscan]].

## Wireshark – filtry

| Filtr | Co ukáže |
| :-- | :-- |
| `arp` | provoz ARP |
| `icmp` | provoz ICMP |
| `!openvpn` | vše kromě provozu VPN |

Viz [[Wireshark]].

## Skenování portů (02 Basic Port Scans)

| Příkaz | Co dělá |
| :-- | :-- |
| `nmap -sT IP` | [[TCP connect scan]] (bez root) |
| `sudo nmap -sS IP` | [[SYN scan]] (výchozí s root) |
| `sudo nmap -sU IP` | [[UDP scan]] (pomalý) |
| `-p22,80,443` / `-p1-1023` / `-p-` | vybrané porty / rozsah / všech 65535 |
| `-F` | rychle, 100 nejběžnějších portů |
| `--top-ports 10` | 10 nejběžnějších portů |
| `-r` | porty postupně, ne náhodně |
| `-T0` až `-T5` | [[časování skenování]] |
| `--min-rate` / `--max-rate N` | pakety za sekundu |
| `--min-parallelism` / `--max-parallelism N` | paralelní sondy |

## Pokročilé skeny (03 Advanced Port Scans)

| Příkaz | Co dělá |
| :-- | :-- |
| `sudo nmap -sN IP` | [[Null scan]] |
| `sudo nmap -sF IP` | [[FIN scan]] |
| `sudo nmap -sX IP` | [[Xmas scan]] |
| `sudo nmap -sM IP` | [[Maimon scan]] |
| `sudo nmap -sA IP` | [[ACK scan]] |
| `sudo nmap -sW IP` | [[Window scan]] |
| `--scanflags URGACKPSHRSTSYNFIN` | [[custom scan]] |
| `-S SPOOFED_IP -e IFACE -Pn` | [[IP spoofing]] |
| `--spoof-mac MAC` | [[MAC spoofing]] |
| `-D IP1,IP2,ME` / `-D RND,RND,ME` | [[decoy scan]] |
| `-f` / `-ff` / `--mtu N` | [[fragmentace paketů]] (8 / 16 bajtů / vlastní) |
| `--data-length N` | připojí náhodná data |
| `--source-port N` | zdrojový port |
| `-sI ZOMBIE_IP` | [[idle scan]] |
| `--reason` | proč Nmap dospěl k závěru |
| `-v` / `-vv` / `-d` / `-dd` | podrobnější výstup / ladění |

## Po skenování portů (04 Post Port Scans)

| Příkaz | Co dělá |
| :-- | :-- |
| `-sV` | [[detekce služeb]] |
| `--version-light` / `--version-all` | intenzita 2 / 9 |
| `-O` | [[detekce OS]] |
| `--traceroute` | trasa k cíli |
| `-sC` / `--script=default` | výchozí skripty ([[NSE]]) |
| `--script "ftp*"` / `--script http-date` | konkrétní skripty |
| `-A` | `-sV -O -sC --traceroute` |
| `-oN` / `-oG` / `-oX` / `-oA` / `-oS` | [[výstupní formáty Nmap]] |
| `grep http soubor.gnmap` | hledání ve výstupu |

## Protokoly (vysvětlení v Computer networking)

[[ARP]] · [[ICMP]] · [[ping]] · [[TCP]] · [[UDP]] · [[DNS]] · [[3-way handshake]] · [[ACK]] · [[IP adresa]] · [[MAC adresa]] · [[firewall]]

## Související

[[nmap]] · [[zjišťování živých hostitelů]] · [[01_Nmap_Live_Host_Discovery|Live Host Discovery]] · [[02_Nmap_Basic_Port_Scans|Basic Port Scans]] · [[03_Nmap_Advanced_Port_Scans|Advanced Port Scans]] · [[04_Nmap_Post_Port_Scans|Post Port Scans]] · [[skenování portů]] · [[stavy portů]]
