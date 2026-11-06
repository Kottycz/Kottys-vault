# Rules

## Přihlašovací údaje

- **Username:** administrator
- **Heslo:** `Pa55w.rd` – u každého účtu
- **Doména:** kotrba.lab

## Síťové karty

Karty se nemusí jmenovat stejně (třeba "Ethernet 1"), ale musí jít za sebou (33, 34, 35).

### NIC1

Připojení do internetu.

### NIC2

Nikam nevede – slouží virtálům, které mezi sebou komunikují přes switch ("pískoviště").

- **Síť:** 192.168.0.0/16
- **Subnet:** 192.168.16.0/24
- **Výchozí brána:** 192.168.16.1/24

### NIC3

Komunikace mezi virtály od sousedů.

## Pojmenování strojů

- **Počítač:** `PC1-WIN` – předloha, číslo pořadí virtálu, operační systém
- **Server:** `SERV1-DC`
![[Pasted image 20260915132615.png|365]]