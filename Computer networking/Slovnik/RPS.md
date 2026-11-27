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

### Proč RPS

Napájecí zdroj je jedna z nejčastěji selhávajících součástek. Switch s jedním zdrojem je [[single point of failure]] pro všechna zařízení na něm. RPS (nebo druhý vestavěný zdroj) to řeší.

### RPS vs. UPS

| | RPS | UPS |
| :-- | :-- | :-- |
| chrání proti | selhání zdroje ve switchi | výpadku elektřiny v síti |
| jak | náhradní zdroj | baterie |

V ideálním případě switch má oboje: RPS na selhání zdroje, UPS na výpadek proudu.

### Barvy LED RPS

| Barva | Význam |
| :-- | :-- |
| nesvítí | RPS není připojen nebo je vypnutý |
| zelená | připojen a připraven |
| bliká zelená | připojen, ale napájí jiné zařízení |
| oranžová | chyba nebo RPS v pohotovosti |

**Souvisí:** [[LED switche]], [[SYST]], [[redundance]], [[single point of failure]], [[switch]]
