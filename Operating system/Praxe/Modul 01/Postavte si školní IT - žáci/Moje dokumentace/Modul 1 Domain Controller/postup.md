# Modul 1 — Domain Controller — postup

> Šablona verze: 2026-10-03 · Vyplňte všechna místa `DOPLNIT`. **Nadpisy ani ID neměňte** — podle nich se vaše práce porovnává se vzorovým řešením. Pravidla viz [[00-pravidla-prace-s-vaultem]].

Ke každé části popište, **co jste skutečně udělali**: kroky v GUI (kde jste klikli, jaké hodnoty jste zadali) nebo příkazy, které jste spustili — v pořadí, jak jste je prováděli. Příkazy vkládejte i s promptem.

## Údaje o řešiteli

| Položka | Hodnota |
|---|---|
| Jméno a příjmení | Matěj Kotrba |
| Třída | T3A |
| Datum vypracování | 25. 10. 2026 |
| Vaše doména | kotrba.cyberschool.internal |

## SRV1-DC

### M1-SRV1.P1 Přidání role AD DS

**M1-SRV1.P1** – Postup — jak jste roli Active Directory Domain Services přidali

```text
Přes Server Manager (Windows PowerShell nemá modul ServerManager, Install-WindowsFeature nefunguje):
Manage -> Add Roles and Features -> Role-based or feature-based installation -> server SRV1-DC
-> Server Roles: Active Directory Domain Services (+ Add Features) -> Next -> Install
```

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [x] Hotovo

### M1-SRV1.P2 Povýšení na řadič domény

**M1-SRV1.P2** – Postup — volby v průvodci: typ nasazení, název domény, NetBIOS jméno, funkční úrovně, volby řadiče, DSRM heslo

```text
Server Manager -> upozornění (vlaječka) -> Promote this server to a domain controller:
- Deployment Configuration: Add a new forest, Root domain name: kotrba.cyberschool.internal
- Domain Controller Options: výchozí funkční úrovně, DNS server + Global Catalog, DSRM heslo Pa55w.rd
- DNS Options: varování o delegaci ignorováno
- Additional Options: NetBIOS name KOTRBA
- Paths a Review Options: výchozí hodnoty -> Install; server se sám restartoval
```

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [x] Hotovo

### M1-SRV1.P3 Přihlášení po restartu

**M1-SRV1.P3** – Postup — jak jste se po restartu přihlásili

```text
Po restartu přihlášení jako KOTRBA\Administrator (heslo Pa55w.rd).
Kontrola: whoami -> kotrba\administrator; (Get-CimInstance Win32_ComputerSystem).Domain -> kotrba.cyberschool.internal; DomainRole -> 5
```

![[m1-srv1-p3-1.png]]

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [x] Hotovo
