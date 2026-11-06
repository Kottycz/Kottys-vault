# Command Structure

Struktura příkazů v [[IOS|Cisco IOS]].

- **Klíčové slovo** – specifický parametr definovaný v operačním systému (např. `ip protocols`).
- **Argument** – není předdefinovaný, je to hodnota nebo proměnná definovaná uživatelem (např. `192.168.10.5`).

Části příkazového řádku: výzva (prompt), příkaz (command), mezera (space), argumenty (arguments).

## Konvence zápisu

| Konvence | Popis |
| :-- | :-- |
| **tučné písmo** | Příkazy a klíčová slova, které zadáváte doslova. |
| *kurzíva* | Argumenty, za které zadáváte vlastní hodnoty. |
| `[ x ]` | Hranaté závorky = volitelný prvek (klíčové slovo nebo argument). |
| `{ x }` | Složené závorky = povinný prvek. |
| `[ x { y \| z } ]` | Složené závorky a svislé čáry v hranatých závorkách = povinná volba v rámci volitelného prvku. |

Mezery se používají k jasnému vymezení částí příkazu.

## Nápověda

- `?` – přístup ke kontextové nápovědě v rozhraní příkazového řádku.
- `Tab` – dokončí částečné zadání názvu příkazu.
