---
aliases: [Secure Shell]
tags: [slovnik]
---

# SSH

**Secure Shell** – protokol pro **šifrované** vzdálené připojení k zařízení (příkazová řádka). Port **22**, běží nad [[TCP]]. Nahrazuje nebezpečný [[Telnet]].

---

## Podrobně

### K čemu slouží

- Vzdálená správa serverů a síťových prvků ([[router|routerů]], [[switch|switchů]])
- Přenos souborů přes **SFTP** nebo SCP
- Tunelování jiných protokolů (port forwarding)

### SSH vs. Telnet

| | SSH | [[Telnet]] |
| :-- | :-- | :-- |
| Šifrování | **ano** | ne |
| Port | 22 | 23 |
| Heslo po síti | šifrované | **čitelné** |
| Dnes | standard | jen v laboratoři |

Telnet posílá všechno včetně hesla v čitelné podobě – kdokoliv s odposlechem ho přečte. Proto se v praxi **vždy** používá SSH.

### Ověřování

| Způsob | Popis |
| :-- | :-- |
| **Heslem** | jednoduché, ale zranitelné vůči hádání |
| **Klíčem** | pár veřejný/soukromý klíč, bezpečnější, nevyžaduje heslo |

### Konfigurace na Cisco

```
Router(config)# hostname R1
Router(config)# ip domain-name kotrba.lab
Router(config)# crypto key generate rsa
Router(config)# username admin secret heslo
Router(config)# line vty 0 4
Router(config-line)# transport input ssh
Router(config-line)# login local
```

Bez hostname a domain-name nejdou vygenerovat klíče – SSH pak nenaběhne.

### SFTP vs. FTPS

- **SFTP** – přenos souborů **přes SSH** (port 22), jiný protokol než FTP
- **FTPS** – klasické [[FTP]] zabalené do [[TLS]] (port 990)

Navzdory podobným názvům to jsou dvě úplně různé věci.

### Ověření a připojení

| Kde | Příkaz |
| :-- | :-- |
| Cisco – stav SSH | `show ip ssh` |
| Cisco – kdo je připojený | `show ssh`, `show users` |
| Windows / Linux – připojení | `ssh admin@192.168.1.1` |
| z Cisco na Cisco | `ssh -l admin 192.168.1.2` |

### Otisk klíče

Při prvním připojení se klient zeptá, jestli věří **otisku klíče** serveru (fingerprint) a uloží si ho. Když se příště otisk změní, klient varuje – buď se na zařízení přegenerovaly klíče, nebo jde o útok ([[MITM]]).

### Omezení přístupu

```
R1(config)# ip ssh time-out 60
R1(config)# ip ssh authentication-retries 2
R1(config)# access-list 5 permit 192.168.99.0 0.0.0.255
R1(config)# line vty 0 4
R1(config-line)# access-class 5 in
```

`access-class` na VTY pustí SSH jen ze sítě adminů.

**Souvisí:** [[Telnet]], [[TCP]], [[port]], [[FTP]], [[TLS]], [[running-config]]
