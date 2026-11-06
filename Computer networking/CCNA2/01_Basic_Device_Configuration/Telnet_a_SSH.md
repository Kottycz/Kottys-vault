# Telnet a SSH

Rozcestník [[Basic_Device_Configuration]]. Viz [[Telnet]], [[SSH]], [[Wireshark]], [[VTY]].

## Telnet

- **TCP port 23**, starý protokol.
- Přenáší **čistým textem** přihlášení (jméno i heslo) i všechna data.
- Útočník s [[Wireshark|Wiresharkem]] v captureu přečte např. username **admin** a heslo **ccna** (Follow TCP Stream).

## SSH

- **TCP port 22**, **šifruje** autentizaci i přenášená data.
- Ve Wiresharku jsou jen „Encrypted packet“, útočník vidí jen IP adresy a provoz, ne obsah.
- V praxi používej **jen SSH**.

## Ověření, že switch umí SSH

[[IOS]] musí obsahovat **kryptografické funkce**: v názvu image je **k9**.

```
S1# show version
Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE7
```

Nebo `show ip ssh` – když IOS SSH nepodporuje, příkaz není rozpoznán.

## Konfigurace SSH (6 kroků)

Předpoklad: unikátní hostname a síťové nastavení ([[SVI]], [[Sprava_switche_SVI]]).

**1. Ověřit podporu SSH:**

```
S1# show ip ssh
```

**2. IP doména:**

```
S1(config)# ip domain-name cisco.com
```

**3. [[RSA]] klíče** (zapne SSH server; modulus 1024, delší = bezpečnější, ale pomalejší generování):

```
S1(config)# crypto key generate rsa
How many bits in the modulus [512]: 1024
```

- Ne všechny IOS defaultně používají SSH v2, SSH v1 má známé slabiny.
- Smazání klíčů (a tím vypnutí SSH serveru): `crypto key zeroize rsa`.

**4. Uživatel (lokální autentizace):**

```
S1(config)# username admin secret ccna
```

**5. [[VTY]] linky:**

```
S1(config)# line vty 0 15
S1(config-line)# transport input ssh
S1(config-line)# login local
S1(config-line)# exit
```

- `transport input ssh` – povolí jen SSH, **Telnet je odříznut**.
- `login local` – autentizace z lokální databáze uživatelů.
- Catalyst 2960 má VTY 0–15.

**6. SSH verze 2:**

```
S1(config)# ip ssh version 2
```

Defaultně jedou obě verze.

## Ověření SSH

- Klient ([[PuTTY]]): Host Name = `172.17.99.11` (SVI S1), port **22**, SSH. PC1 má `172.17.99.21`.
- Přihlášení: `admin` / `ccna`, pak `enable`.

```
S1# show ip ssh
SSH Enabled - version 2.0
Authentication timeout: 120 secs; Authentication retries: 3

S1# show ssh
Connection Version Mode Encryption Hmac       State            Username
0          2.0     IN   aes256-cbc hmac-sha1  Session started  admin
0          2.0     OUT  aes256-cbc hmac-sha1  Session started  admin
```

Související: [[Zakladni_konfigurace_zarizeni]] (hesla, VTY v CCNA1), [[banner MOTD]]
