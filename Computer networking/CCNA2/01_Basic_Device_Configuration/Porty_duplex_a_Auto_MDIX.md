# Porty: duplex, rychlost a Auto-MDIX

Rozcestník [[Basic_Device_Configuration]]. Viz [[duplex]], [[Ethernet]], [[auto-negotiation]].

## Duplex

- **[[full-duplex]]** – vysílání i příjem **současně**, oba směry 100 % efektivní, bez [[kolize|kolizí]].
- **[[half-duplex]]** – jednosměrná komunikace, data jen v jednom směru najednou, **kolize**, horší výkon. Typicky staré **huby**; nahradily je switche, které jedou full-duplex.

[[Optické vlákno|Optické]] porty (např. 1000BASE-SX) mají jednu pevnou rychlost a jsou **vždy full-duplex**.

## Auto-negotiation

- Port umí half- i full-duplex při 10/100 Mb/s, při **1000 Mb/s jen full-duplex**.
- [[auto-negotiation|Auto]] je vhodné, když nevíš, co je na druhé straně.
- U známých zařízení (servery, switche, routery) je best practice **nastavit ručně** duplex i rychlost.
- **Pozor:** nesoulad duplexu/rychlosti = problémy s konektivitou, selhání auto-negotiation vytvoří nesoulad. Při troubleshootingu vždy zkontrolovat duplex a rychlost (viz [[late collision]]).

## Nastavení portu

Příklad: S1 a S2, F0/1, full-duplex 100 Mb/s.

```
S1# configure terminal
S1(config)# interface FastEthernet 0/1
S1(config-if)# duplex full
S1(config-if)# speed 100
S1(config-if)# end
S1# copy running-config startup-config
```

Totéž na S2.

## Auto-MDIX

[[Auto-MDIX]]: switch sám pozná typ kabelu (**přímý** vs. **křížený**) a spojení přizpůsobí. Bez Auto-MDIX: přímý kabel k serverům, PC, routerům; křížený mezi switche.

```
S1(config-if)# mdix auto
```

- Rychlost i duplex na rozhraní musí být **auto**, jinak to nefunguje.
- Na Catalyst **2960 a 3560 je zapnuto defaultně**, na starých 2950 a 3550 **není**.

Kontrola:

```
S1# show controllers ethernet-controller fa0/1 phy | include MDIX
Auto-MDIX   : On   [AdminState=1   Flags=0x00052248]
```

Související: [[LED switche]] (LED DUPLX a SPEED), [[Overovani_switche_a_chyby_rozhrani]]
