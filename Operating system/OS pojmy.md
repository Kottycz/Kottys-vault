# OS pojmy – rozcestník

Přehled pojmů ve Slovníku, roztříděný podle témat.

## Hardware

- [[CPU]], [[registr]], [[cache]]
- [[RAM]], [[ROM]], [[EEPROM]], [[HDD]], [[SSD]], [[RPM]], [[SLC-MLC]]
- [[řadič]], [[DMA]], [[PIO]]
- [[BIOS]], [[firmware]], [[bootstrap]], [[POST]]

## Jádro

- [[operační systém]], [[kernel]]
- [[přerušení]], [[systémové volání]]

## Procesy a vlákna

- [[proces]], [[vlákno]], [[PCB]], [[PID]]
- [[fork-exec]], [[zombie proces]]
- [[plánování procesů]], [[SMP]]
- [[přepnutí kontextu]], [[swapping]]

## Synchronizace

- [[kritická sekce]], [[semafor]], [[mutex]]
- [[uváznutí]], [[starvation]]

## IPC

- [[IPC]], [[pipe]]

## Paměť

- [[virtuální paměť]], [[MMU]], [[heap]]

## Úložiště a souborové systémy

- [[žurnálování]], [[RAID]], [[FCB]], [[i-node]], [[NFS]], [[LDAP]]

## Rozhraní a standardy

- [[GUI]], [[CLI]], [[API]]
- [[POSIX]]

## Datové struktury

- [[pole]], [[spojový seznam]]
- [[zásobník]], [[fronta]]
- [[hašovací tabulka]], [[BST]]

## Praxe – Windows Server

- příprava: [[VM]], [[hypervizor]], [[snapshot]], [[Server Core]], [[MMC]], [[KMS]], [[LAB KEY]], [[CAL]], [[OOBE]]
- identita a čas: [[FQDN]], [[NetBIOS]], [[UTC]], [[NTP]], [[Kerberos]], [[MFA]]
- doména: [[AD DS]], [[SAM]], [[řadič domény]], [[FSMO]], [[Global Catalog]], [[RODC]], [[USN rollback]], [[NTDS.dit]], [[SYSVOL]], [[Netlogon]]
- objekty: [[OU]], [[ADUC]], [[GPO]], [[DN]], [[UPN]], [[SID]], [[ACL]], [[AGDLP]], [[kočovný profil]], [[secure channel]]
- DHCP: [[DHCP scope]], [[lease]], [[APIPA]], [[rogue DHCP]], [[DHCP relay]]
- DNS: [[DNS záznam]], [[reverzní DNS]], [[SRV záznam]], [[DNS přípona]], [[DNS TTL]], [[TLD]], [[ICANN]], [[forwarder]], [[zone transfer]], [[scavenging]], [[mDNS]], [[NXDOMAIN]], [[DNSSEC]], [[DoH]], [[CA]], [[SPF-DKIM-DMARC]]
- moduly: [[00_Priprava_OS]], [[01_AD_DS]], [[02_DHCP]], [[03_DNS]]

### Teorie k modulům

- **00 Příprava:** [[00a_Virtualizace_edice_aktivace]], [[00b_Identita_a_sit]], [[00c_Cas_jazyk_soukromi]]
- **01 Domain Controller:** [[01a_Domena_a_AD]], [[01b_Radice_domeny_a_FSMO]], [[01c_Jmeno_domeny_a_DNS]]
- **02 DHCP:** [[02a_DHCP_teorie]]
- **03 DNS:** [[03a_DNS_obecne]], [[03b_DNS_na_radici]]
- **04 Active Directory:** [[04a_Navrh_OU]], [[04b_Skupiny_a_AGDLP]], [[04c_Ucty_a_pripojeni_PC]]
