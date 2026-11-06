# Tor

## [[tor|TOR]] (The Onion Router)

### [[onion_routing|Onion routing]] (cibulové směrování)

Data uživatele jsou zašifrována ve více vrstvách šifrování (jako vrstvy cibule). Každá vrstva odpovídá jednomu uzlu v TOR síti – na každém uzlu se odstraní jedna vrstva šifrování, čímž se odhalí jen další cílový uzel, ne celá trasa.

### Struktura TOR sítě

Síť tvoří tisíce dobrovolných uzlů, rozdělených na:

- **vstupní/guard uzel** – první uzel, kam se klient připojí
- **střední/middle uzly** – několik uzlů uprostřed trasy
- **výstupní/exit uzel** – poslední uzel, odtud jde nešifrovaně dál na cílovou adresu

Žádný jednotlivý uzel nezná celou trasu najednou (uzel 1 zná IP klienta a uzel 2, uzel 2 zná uzel 1 a uzel 3, uzel 3 zná jen uzel 2 a cíl) – díky tomu je těžké dohledat původ i cíl komunikace.

### Jak probíhá připojení

1. **Připojení k síti** – klient se nejdřív nešifrovaně spojí s adresářovým serverem (seznam uzlů), pak se šifrovaně připojí přes náhodný vstupní, střední a výstupní uzel k cíli
2. **Změna tras** – vstupní uzel se mění zhruba každých 10 minut, aby nešlo připojení odhalit statistickou analýzou
3. **Zvýšení anonymity provozováním vlastního uzlu** – když uživatel sám funguje i jako uzel pro cizí provoz, nejde zvenčí rozeznat, jestli je připojení jeho vlastní, nebo jen přeposílané

### Nevýhody TOR

- **pomalost** – uzly jsou po celém světě, odezva je horší než u proxy/VPN
- **zneužívání** – často se využívá k nelegální činnosti (brute force, zneužívání zranitelností)
- **exit uzly na blacklistech** – velcí poskytovatelé CDN je blokují nebo vyžadují captchu
- **DDoS útoky** na exit uzly, které mohou destabilizovat síť

## Tor Browser

Upravený Mozilla Firefox, který zjednodušuje připojení do sítě TOR (nastaví vše potřebné automaticky).

## [[dark_web|Deep web / Dark web]]

Stránky na doménách **.onion**, dostupné jen přes Tor Browser (potřeba znát přesnou adresu). Adresy se hledají přes rozcestníky jako **Hidden Wiki**. Na dark webu prakticky neplatí žádná pravidla ani omezení – i jen procházení může vzbudit podezření z nelegální činnosti.





# Soukromí na internetu
## [[fingerprinting|Fingerprinting]] prohlížeče

"Otisk prstu" prohlížeče – jedinečná kombinace technických údajů (model zařízení, operační systém, systémový font, rozložení klávesnice, verze prohlížeče, časové pásmo, jazyk, blokovač reklam, rozlišení obrazovky, CPU, grafická karta…), podle které lze uživatele rozpoznat i bez cookies. Na rozdíl od cookies se nemění mezi anonymním prohlížením ani po smazání dat prohlížeče.

Nástroje na ověření vlastního fingerprintu: [amiunique.org](https://amiunique.org/), [coveryourtracks.eff.org](https://coveryourtracks.eff.org/)

## Zdroj

TryHackMe – *Tor a soukromí na internetu*; TryHackMe – *MTA-SOUKROMÍ V KYBERPROSTORU*; TryHackMe – *MTA-TOR*
