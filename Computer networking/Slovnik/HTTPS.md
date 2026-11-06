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

**Souvisí:** [[HTTP]], [[TCP]], [[port]]
