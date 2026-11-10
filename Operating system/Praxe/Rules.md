# Rules

## Přihlašovací údaje

- **Username:** administrator
- **Heslo:** `Pa55w.rd` – u každého účtu
- **Doména:** kotrba.cyberschool.internal

## Síťové karty

Karty se nemusí jmenovat stejně (třeba "Ethernet 1"), ale musí jít za sebou (33, 34, 35).

### NIC1

Připojení do internetu (NAT). Ve Windows je to obvykle `Ethernet0`.

> [!warning] Na NIC1 (Ethernet0) nikdy nesahat
> Neměnit na ní IP adresu, bránu ani DNS a nevypínat ji. Přes tuhle kartu se k virtuálu připojujeme a má internet, takže by šlo o přístup ke stroji přijít. Veškerá komunikace uvnitř učebny (DHCP, DNS, doména, ping mezi stroji) probíhá **výhradně na NIC2** (ve Windows `Ethernet1`). Při příkazech vždy uvádět `-InterfaceAlias Ethernet1` nebo `/release Ethernet1`.

### NIC2

Nikam nevede – slouží virtálům, které mezi sebou komunikují přes switch ("pískoviště").

- **Síť:** 192.168.0.0/16
- **Subnet:** 192.168.16.0/24
- **Výchozí brána:** 192.168.16.1/24

### NIC3

Komunikace mezi virtály od sousedů.

## Pojmenování strojů

- **Počítač:** `PC1-WIN` – předloha, číslo pořadí virtálu, operační systém
- **Server:** `SRV1-DC` - domain control     `SRV2-FS` - filesystem

![[Pasted image 20260915132615.png|365]]

## Moduly

- [[00_Priprava_OS|Modul 00 – Příprava a instalace OS]]
- [[01_AD_DS|Modul 01 – Active Directory]]
- [[02_DHCP|Modul 02 – DHCP]]
- [[03_DNS|Modul 03 – DNS]]
