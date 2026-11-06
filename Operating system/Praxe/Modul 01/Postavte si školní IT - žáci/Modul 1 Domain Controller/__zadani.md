# [Co má být na konci modulu a jak to vypadá?]

> Verze: 2026-10-03

**Přibližný potřebný čas**: 2 vyučovací hodiny

## Kontext (proč to děláme)

Paní učitelka **Nováková** má dost přihlašování na "univerzální" lokální účty typu `ucitel`/`ucitel`, které zná celá škola. Chce, aby každý žák a učitel měl **svůj vlastní** účet, který funguje na libovolném počítači ve škole. To je přesně to, co řeší Active Directory Domain Services.

## Předpoklad: server je připravený (Modul 0)

Tento modul předpokládá, že server **SRV1-DC** už prošel [[../Modul 0 Příprava/__zadani|Modulem 0 — Příprava]]: má nainstalovaný Windows Server 2025 Datacenter (Desktop Experience), hostname `SRV1-DC`, statickou IP `192.168.200.10/24`, účet `Administrator`/`Pa55w.rd` a hotovou lokalizaci (anglické rozhraní, česká regionální nastavení a klávesnice, časové pásmo Praha). Pokud jste Modul 0 ještě neudělali, vraťte se k němu první.

## Povýšení na řadič domény

Server SRV1-DC bude mít nainstalovanou roli **Active Directory Domain Services (AD DS)** a bude povýšen na řadič nového lesa a domény `prijmeni.cyberschool.internal`.

- Doména `prijmeni.cyberschool.internal` existuje a SRV1-DC je jejím řadičem (Domain Controller). Za `prijmeni` je dosazené vaše příjmení bez diakritiky, malými písmeny (např. `novak.cyberschool.internal`); NetBIOS jméno domény je odvozené automaticky (např. `NOVAK`).
- SRV1-DC je prvním řadičem nového lesa: drží všech pět rolí **FSMO** a je **Global Catalog**.
- Server zároveň funguje jako DNS server pro tuto doménu (role DNS se instaluje automaticky spolu s AD DS).
- Po restartu se přihlašujete jako `Administrator@prijmeni.cyberschool.internal` (nikoliv jen lokálně).

> 📷 **Screenshot sem:** [Server Manager — Local Server, položka Domain s hodnotou prijmeni.cyberschool.internal]

## Ověření nástroji

Na SRV1-DC jsou dostupné administrační nástroje pro správu domény — **Active Directory Users and Computers**, **DNS Manager**, **Active Directory Domains and Trusts** — přístupné přes Server Manager → Tools.
