---
aliases: [Redundant Power System]
tags: [slovnik]
---

# RPS

**RPS** (Redundant Power System) – **záložní napájecí zdroj** pro switch; když vlastní zdroj selže, RPS ho nahradí. Příklad: výpadek zdroje ve switchi, RPS drží síť v chodu.

---

## Podrobně

### LED RPS na switchi

| Stav LED | Význam |
| :-- | :-- |
| vypnuto | RPS je vypnutý nebo není správně připojen |
| **zelená** | RPS připojen a připraven poskytnout zálohu |
| **blikající zelená** | RPS připojen, ale **nedostupný** – právě napájí jiné zařízení |
| **oranžová** | RPS je ve standby nebo v chybě |
| **blikající oranžová** | **vlastní zdroj switche selhal** a napájí RPS |

Princip je [[redundance]] – eliminace [[single point of failure]] v napájení.

**Souvisí:** [[LED switche]], [[SYST]], [[redundance]], [[single point of failure]], [[switch]]
