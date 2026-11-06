---
aliases: [key log file, soubor s klíči, TLS keylog]
tags: [slovnik]
---

# SSLKEYLOGFILE

Proměnná prostředí / soubor, do kterého prohlížeč **ukládá TLS klíče** – Wireshark s ním umí **dešifrovat HTTPS**.

*Příklad: `SSLKEYLOGFILE=C:\keys.txt`, pak ve Wiresharku Edit → Preferences → Protocols → TLS → (Pre)-Master-Secret log filename.*

---

## Podrobně

- funguje s **Chrome** a **Firefox**
- klíče jsou **pro každou relaci zvlášť** → musí se ukládat **během zachytávání**, zpětně nejdou
- přidání: pravý klik na TLS paket nebo **Edit → Preferences → Protocols → TLS**
- po dešifrování jsou vidět HTTP/2 pakety, hlavičky a data

**Souvisí:** [[TLS]], [[HTTPS]], [[Wireshark]]
