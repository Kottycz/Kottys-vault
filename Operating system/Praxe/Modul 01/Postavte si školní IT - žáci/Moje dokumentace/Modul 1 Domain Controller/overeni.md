# Modul 1 — Domain Controller — ověření

> Šablona verze: 2026-10-03 · Vyplňte všechna místa `DOPLNIT`. **Nadpisy ani ID neměňte** — podle nich se vaše práce porovnává se vzorovým řešením. Pravidla viz [[00-pravidla-prace-s-vaultem]].

Ke každému bodu z [[Modul 1 Domain Controller/_vysledek|výsledku modulu]] vložte **důkaz**, že je splněný. Textové výpisy vkládejte i s promptem (datum, čas, účet, počítač), screenshoty s viditelnými hodinami na hlavním panelu.

## Údaje o řešiteli

| Položka | Hodnota |
|---|---|
| Jméno a příjmení | Matěj Kotrba |
| Třída | T3A |
| Datum vypracování | 25. 10. 2026 |
| Vaše doména | kotrba.cyberschool.internal |

## SRV1-DC

### M1-SRV1.V0 Otisk (nehodnotí se, ale je povinný)

Spusťte na SRV1-DC po povýšení na řadič domény. SID domény je jedinečný pro každou instalaci lesa. Spusťte v PowerShellu tyto příkazy a vložte celý výstup i s promptem:

```powershell
Get-Date
whoami
hostname
(Get-CimInstance Win32_ComputerSystemProduct).UUID
(Get-ADDomain).DNSRoot
(Get-ADDomain).DomainSID.Value
```

**M1-SRV1.V0-O** – Otisk

![[m1-srv1-v0-1.png]]

![[m1-srv1-v0-3.png]]

![[m1-srv1-v0-2.png]]

- [x] Hotovo

### M1-SRV1.V1 Server dostupný v síti

**M1-SRV1.V1-D1** – Důkaz: IP konfigurace serveru

![[m1-srv1-v1-1.png]]

- [x] Hotovo

### M1-SRV1.V2 Role AD DS a DNS

**M1-SRV1.V2-D1** – Důkaz: Server Manager — Dashboard s rolemi AD DS a DNS bez chyb

![[m1-srv1-v2-1.png]]

- [x] Hotovo

### M1-SRV1.V3 Server je řadičem domény

**M1-SRV1.V3-D1** – Důkaz: Server Manager — Local Server, položka Domain s vaší doménou

![[m1-srv1-v3-1.png]]

- [x] Hotovo

### M1-SRV1.V4 Role FSMO a Global Catalog

**M1-SRV1.V4-D1** – Důkaz: Držitelé všech pěti rolí FSMO

![[m1-srv1-v4-1.png]]

**M1-SRV1.V4-D2** – Důkaz: Vlastnosti řadiče domény: doména, les, Global Catalog, role

![[m1-srv1-v4-3.png]]

![[m1-srv1-v4-2.png]]

- [x] Hotovo

### M1-SRV1.V5 Nástroje pro správu domény

**M1-SRV1.V5-D1** – Důkaz: ADUC s otevřenou vaší doménou a výchozími kontejnery

![[m1-srv1-v5-1.png]]

- [x] Hotovo

### M1-SRV1.V6 Restart nic nerozbije

**M1-SRV1.V6-D1** – Důkaz: Přihlášený účet po restartu a stav rolí

![[m1-srv1-v6-1.png]]

![[m1-srv1-v6-2.png]]

- [x] Hotovo
