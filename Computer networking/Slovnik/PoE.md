---
aliases: [Power over Ethernet]
tags: [slovnik]
---

# PoE

**PoE** (Power over Ethernet) – napájení zařízení **přímo po ethernetovém kabelu** ze switche; není potřeba zvláštní adaptér. Příklad: IP telefon, Wi-Fi [[AP]] nebo kamera dostane proud z portu switche.

---

## Podrobně

- Switch musí PoE podporovat; LED **PoE** je na switchi jen u modelů s touto funkcí.
- Switch hlídá celkový příkon – když by další zařízení překročilo kapacitu, port odmítne.

### LED PoE (v režimu PoE tlačítkem Mode)

| LED | Význam |
| :-- | :-- |
| PoE LED vypnuta | režim PoE není zvolen a žádný port nebyl odmítnut |
| PoE LED **blikající oranžová** | režim není zvolen, ale aspoň jednomu portu byl odepřen proud nebo má PoE chybu |
| PoE LED **zelená** | režim zvolen, LED portů ukazují stav PoE |

**LED portu v režimu PoE:**

- vypnuta = PoE vypnuto,
- **zelená** = PoE zapnuto,
- **střídavě zelená–oranžová** = PoE odepřeno (příkon by překročil kapacitu switche),
- **blikající oranžová** = PoE vypnuto kvůli chybě,
- **oranžová** = PoE na portu zakázáno.

**Souvisí:** [[LED switche]], [[SYST]], [[switch]], [[AP]], [[Ethernet]]
