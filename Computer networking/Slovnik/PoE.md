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

### Standardy

| Standard | Název | Max. výkon na portu switche |
| :-- | :-- | :-- |
| 802.3af | PoE | 15,4 W |
| 802.3at | PoE+ | 30 W |
| 802.3bt | PoE++ | 60 W / 90 W |

Na zařízení dojde o něco méně, část výkonu se ztratí v kabelu.

### Co se napájí přes PoE

IP telefony, [[AP|Wi-Fi access pointy]], IP kamery, malé switche, osvětlení. Výhoda: stačí jeden kabel, není potřeba zásuvka u každého zařízení, a když má switch záložní napájení, fungují i telefony při výpadku proudu.

### Rozpočet výkonu

Switch má omezený celkový výkon pro PoE (PoE budget). Když se připojí moc zařízení, některá nedostanou napájení. Ověření na Cisco: `show power inline`.

**Souvisí:** [[LED switche]], [[SYST]], [[switch]], [[AP]], [[Ethernet]]
