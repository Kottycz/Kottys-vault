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

**Souvisí:** [[startup-config]], [[SVI]], [[switch]], [[router]]
