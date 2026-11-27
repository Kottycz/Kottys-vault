---
aliases: [běžící konfigurace, running config]
tags: [slovnik]
---

# running-config

**Aktuálně běžící konfigurace** zařízení, uložená v paměti **RAM**. Každá provedená změna se do ní projeví okamžitě – ale po restartu se ztratí.

---

## Podrobně

### Dvě konfigurace na zařízení

| | running-config | [[startup-config]] |
| :-- | :-- | :-- |
| Uložena v | RAM | NVRAM |
| Kdy platí | právě teď | načte se při startu |
| Přežije restart | **ne** | ano |
| Mění se | při každém příkazu | jen při uložení |

### Zobrazení

```
Switch# show running-config
Switch# show startup-config
```

### Uložení změn

```
Switch# copy running-config startup-config
```

nebo zkráceně:

```
Switch# write memory      (nebo jen  wr)
```

**Tohle je nejčastější chyba začátečníků** – nakonfiguruješ zařízení, restartuješ ho a všechno je pryč, protože se to neuložilo.

### Opačný směr – zahození změn

Když něco pokazíš a ještě jsi to neuložil, stačí zařízení restartovat (`reload`) – načte se poslední uložená startup-config a změny zmizí.

```
Switch# copy startup-config running-config
```

tohle naopak **nefunguje jako návrat zpět** – konfigurace se sloučí, nepřepíše. Pro čistý návrat je lepší `reload`.

### Smazání konfigurace

```
Switch# erase startup-config
Switch# reload
```

Zařízení nastartuje s tovární konfigurací.

### Porovnání running a startup

| | running-config | [[startup-config]] |
| :-- | :-- | :-- |
| paměť | RAM | NVRAM (router), flash (switch) |
| po restartu | zmizí | zůstane |
| změny | projeví se hned | jen po uložení |

### Záloha konfigurace

```
R1# copy running-config tftp:
Address or name of remote host []? 192.168.1.100
Destination filename [r1-confg]?
```

Nebo jednoduše `show running-config`, výpis zkopírovat z terminálu do textového souboru.

### Hesla v konfiguraci

Hesla zadaná přes `password` jsou v running-config čitelná. Příkaz `service password-encryption` je zašifruje slabou šifrou (typ 7), aby nebyla vidět přes rameno. Pro enable heslo se používá `enable secret` (silný hash).

**Souvisí:** [[startup-config]], [[SVI]], [[switch]], [[router]]
