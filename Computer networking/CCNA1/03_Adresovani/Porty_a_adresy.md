# Porty a adresy

## IP adresy

Každé koncové zařízení v síti musí být nakonfigurováno s IP adresou.

Struktura [[IPv4]] adresy se nazývá **tečkovaná desítková notace** – čtyři desítková čísla mezi 0 a 255.

Zjištění vlastní IP adresy: příkaz `ipconfig`.

**Maska podsítě IPv4** je 32bitová hodnota, která odlišuje síťovou část adresy od hostitelské. Spolu s IPv4 adresou určuje, do které podsítě je zařízení členem.

**Adresa [[default gateway|výchozí brány]]** je [[IP adresa]] [[router|routeru]], který hostitel použije pro přístup ke vzdáleným sítím včetně internetu.

## Rozhraní a porty

Při volbě média se zvažuje:
- vzdálenost, na kterou může médium úspěšně přenášet signál,
- prostředí, ve kterém má být médium instalováno,
- množství dat a rychlost, s jakou musí být přenášena,
- cena média a instalace.

Ethernet je dnes nejběžnější technologií lokálních sítí ([[LAN]]).

Přepínače mají jedno nebo více **virtuálních rozhraní [[switch|přepínače]] ([[SVI]])**. Virtuální rozhraní umožňuje vzdáleně spravovat přepínač přes síť pomocí IPv4 a [[IPv6]].

**Poznámka:** Switch vrstvy 2 nepotřebuje IP adresu. IP adresa přiřazená rozhraní SVI slouží jen pro vzdálený přístup k switchi – pro samotné operace přepínače není nezbytná.
