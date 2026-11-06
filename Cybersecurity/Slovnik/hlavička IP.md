---
aliases: [IP hlavička, IP header]
tags: [slovnik]
---

# Hlavička IP

Úvodní část IP paketu s **adresami, IP ID, ofsetem fragmentu** a dalšími údaji; minimálně 20 bajtů.

*Příklad: zdrojová a cílová adresa mají po 4 bajtech.*

---

## Podrobně

- zdrojová IP – 32 bitů (4 bajty), cílová – dalších 32 bitů
- **IP ID** a **ofset fragmentu** slouží ke složení fragmentů
- firewall ji kontroluje vždy

**Souvisí:** [[IP ID]], [[IP adresa]], [[fragmentace paketů]], [[hlavička TCP]], [[firewall]]
