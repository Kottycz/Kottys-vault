---
aliases: [Escape sekvence]
tags: [slovnik]
---

# escape sekvence

**Speciální znaky uvnitř textu**, které začínají zpětným lomítkem `\` – třeba `\n` je nový řádek.

```csharp
Console.Write("roman\n\n");   // "roman" + 2 nové řádky
```

---

## Podrobně

### Proč existují

Některé znaky nejde do textu napsat normálně – buď nejsou vidět (odřádkování, tabulátor), nebo mají v kódu jiný význam (uvozovka by ukončila string). Zpětné lomítko říká: "následující znak ber speciálně".

### Přehled

| Sekvence | Význam | Příklad | Výstup |
| :-- | :-- | :-- | :-- |
| `\n` | nový řádek | `"a\nb"` | a<br>b |
| `\t` | tabulátor | `"a\tb"` | a    b |
| `\"` | uvozovka | `"řekl \"ahoj\""` | řekl "ahoj" |
| `\'` | apostrof (v [[char]]) | `'\''` | ' |
| `\\` | zpětné lomítko | `"C:\\Users"` | C:\Users |

### Tabulátor na zarovnání

```csharp
Console.WriteLine("jméno\tvěk");
Console.WriteLine("Kotty\t17");
```

### Doslovný string `@`

Když je v textu hodně lomítek (cesty k souborům), jde před uvozovky dát `@` – escape sekvence se pak nepoužívají:

```csharp
string cesta = @"C:\Users\kotrb\Documents";   // bez zdvojování \\
```

**Souvisí:** [[string]], [[char]], [[write]], [[writeline]]
