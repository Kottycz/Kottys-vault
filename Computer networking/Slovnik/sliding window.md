---
aliases: [posuvné okno, okno]
tags: [slovnik]
---

# sliding window

**Posuvné okno** – mechanismus [[TCP]] pro **řízení toku**. Příjemce oznamuje, kolik dat ještě zvládne přijmout, a odesílatel víc neposílá.

---

## Podrobně

### Proč je potřeba

Rychlý server by zahltil pomalého klienta – data by se ztrácela, protože by se nevešla do bufferu. Okno tomu brání.

### Jak funguje

V hlavičce TCP je pole **Window** – volné místo v bufferu příjemce v bajtech:

```
Příjemce: "mám volných 4000 B"  → Window = 4000
Odesílatel pošle max 4000 B a čeká na potvrzení (ACK)
Příjemce data zpracuje, uvolní buffer, pošle nové Window
Okno se "posune" a odesílatel může poslat další data
```

Odesílatel tak může mít **víc nepotvrzených segmentů na cestě zároveň** – nečeká na potvrzení každého zvlášť, což by bylo strašně pomalé.

### Dynamická změna

Okno se během spojení mění:
- příjemce nestíhá → okno se zmenší → odesílatel zpomalí
- příjemce má volno → okno se zvětší → přenos zrychlí
- okno = 0 → odesílatel musí úplně počkat

### Řízení toku vs. řízení zahlcení

Snadno se to plete:

| | Co chrání | Řídí |
| :-- | :-- | :-- |
| **Sliding window** (řízení toku) | příjemce | příjemce oknem |
| **[[slow start]]** (řízení zahlcení) | síť mezi nimi | odesílatel podle ztrát |

Odesílatel se řídí **menším** z obou limitů.

### Ukázka

Příjemce oznámí okno **3000 B**, segmenty mají 1000 B:

```
odešlu 1, 2, 3          ← okno plné, čekám
přijde ACK za 1         ← okno se posune
odešlu 4
přijde ACK za 2 a 3
odešlu 5, 6
```

Odesílatel nečeká na potvrzení každého segmentu zvlášť. Smí mít „ve vzduchu" tolik nepotvrzených dat, kolik je okno.

### Okno nula

Když příjemce nestíhá (plný buffer), pošle **window = 0**. Odesílatel přestane posílat a jen občas zkusí malou sondu (window probe), jestli už se místo uvolnilo.

### Ve Wiresharku

V každém TCP segmentu je pole **Window size value**. Wireshark upozorní na `TCP ZeroWindow` a `TCP Window Full`. To ukazuje, že zpomaluje příjemce, ne síť.

**Souvisí:** [[TCP]], [[slow start]], [[MSS]], [[3-way handshake]]
