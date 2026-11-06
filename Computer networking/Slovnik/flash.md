---
aliases: [flash paměť, flash:]
tags: [slovnik]
---

# flash

**Flash** – trvalá paměť zařízení Cisco, ve které je uložený samotný [[IOS]]. Přežije restart i vypnutí. Příklad: soubor `c2960-lanbasek9-mz.150-2.SE8.bin` ve flash.

---

## Podrobně

### Paměti zařízení Cisco

| Paměť | Obsah | Přežije restart |
| :-- | :-- | :-- |
| **Flash** | IOS | ano |
| RAM | [[running-config]] | ne |
| NVRAM | [[startup-config]] | ano |
| ROM | [[boot loader]], bootovací instrukce | ano |

### Příkazy

```
S1# show flash
S1# dir flash:
```

V [[boot loader|boot loaderu]]: `flash_init` (inicializace) a pak `dir flash:`.

### K čemu

- uložení a **výměna IOS** (nový obraz, záloha),
- boot proměnná `BOOT=flash:...` ukazuje, který soubor se načte.

**Souvisí:** [[IOS]], [[boot loader]], [[POST]], [[running-config]], [[startup-config]]
