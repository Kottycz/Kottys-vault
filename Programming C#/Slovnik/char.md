---
aliases: [char, Char]
tags: [slovnik]
---

# char

**Jeden znak** (písmeno, číslice, symbol). Píše se do **jednoduchých** uvozovek.

```csharp
char d = 'A';
```

---

## Podrobně

### Vlastnosti

| | Hodnota |
| :-- | :-- |
| Velikost | 16 bitů (2 bajty) |
| Kódování | Unicode (UTF-16) – umí i `'č'`, `'ř'` |
| Výchozí hodnota | `'\0'` (nulový znak) |

### char vs. string

| | `char` | [[string]] |
| :-- | :-- | :-- |
| Uvozovky | jednoduché `'A'` | dvojité `"A"` |
| Obsah | přesně 1 znak | libovolný počet znaků (i 0) |

`'A'` a `"A"` **nejsou** stejné – nejde je přímo porovnat ani přiřadit jedno do druhého.

### Znak je vlastně číslo

Každý znak má v tabulce Unicode své číselné pořadí – `'A'` je 65, `'B'` 66, `'a'` 97. Proto s ním jde počítat:

```csharp
int kod = 'A';          // 65
char dalsi = (char)('A' + 1);   // 'B'
```

### Znak ze stringu

Jednotlivé znaky řetězce se dají vytáhnout indexem (od 0):

```csharp
string jmeno = "Kotty";
char prvni = jmeno[0];   // 'K'
```

### Speciální znaky

Zapisují se přes [[escape_sekvence|escape sekvence]]: `'\n'` (nový řádek), `'\''` (apostrof), `'\\'` (zpětné lomítko).

**Souvisí:** [[datovy_typ]], [[string]], [[escape_sekvence]], [[pretypovani]]
