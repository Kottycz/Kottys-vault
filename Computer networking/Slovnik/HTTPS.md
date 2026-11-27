---
aliases: [HTTP Secure, HyperText Transfer Protocol Secure]
tags: [slovnik]
---

# HTTPS

**HTTP Secure** – zabezpečená verze [[HTTP]]. Běží nad [[TCP]] na portu **443**, obsah šifruje pomocí TLS (dříve SSL) a ověřuje identitu serveru certifikátem.

---

## Podrobně

### Co přidává oproti HTTP

HTTPS = HTTP + **TLS**. Zajišťuje tři věci:

1. **Důvěrnost** – obsah je zašifrovaný, po cestě ho nikdo nepřečte
2. **Integrita** – data nelze cestou nepozorovaně změnit
3. **Autenticita** – certifikát ověří, že server je opravdu ten, za koho se vydává (ne podvržený web)

### TLS handshake (zjednodušeně)

1. Klient se připojí a pošle, jaké šifry umí
2. Server pošle svůj **certifikát** s veřejným klíčem
3. Klient ověří certifikát proti důvěryhodné certifikační autoritě (CA)
4. Obě strany se dohodnou na symetrickém klíči pro relaci
5. Od této chvíle jde všechno šifrovaně

Teprve potom začne samotná HTTP komunikace (GET, POST…).

### Certifikát a certifikační autorita

Certifikát vydává **CA** (certifikační autorita, např. Let's Encrypt). Prohlížeč má v sobě seznam důvěryhodných CA – když certifikát nesedí (vypršel, je pro jinou doménu, vydala ho neznámá CA), zobrazí varování.

### Co HTTPS neskrývá

- **Doménu**, na kterou se připojuješ (viditelná v [[DNS]] dotazu a v SNI)
- **IP adresy** obou stran
- Objem a načasování provozu

Skrývá ale konkrétní URL, obsah stránky, hesla a odeslaná data.

### TLS vs. SSL

SSL je starší, dnes už nebezpečný a nepoužívaný protokol. Název "SSL" se ale pořád používá hovorově pro TLS (např. "SSL certifikát" = ve skutečnosti TLS).

### Jak poznat HTTPS v prohlížeči

- adresa začíná `https://`,
- u adresy je ikona zámku, kliknutím zobrazíš certifikát (kdo ho vydal, pro jakou doménu, do kdy platí),
- varování o neplatném certifikátu = buď chyba na webu, nebo někdo provoz zachytává ([[MITM]]). Nepokračovat.

### Šifrování: dva druhy klíčů

- **asymetrické** (veřejný a soukromý klíč, [[RSA]] nebo ECDHE) – jen na začátku, k bezpečné domluvě společného klíče,
- **symetrické** (např. AES) – jedním společným klíčem se pak šifrují všechna data, protože je to mnohem rychlejší.

### HTTPS a firewall

Firewall vidí, že komunikuješ s IP serveru na portu 443, a ze jména v certifikátu i na jaký web. Obsah stránek ale nevidí. Firmy proto někdy HTTPS na hranici sítě rozšifrovávají (SSL inspection), na firemní PC k tomu instalují vlastní certifikát.

**Souvisí:** [[HTTP]], [[TCP]], [[port]]
