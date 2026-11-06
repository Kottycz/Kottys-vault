# Síťové komponenty

## Hostitelské role

Termín **hostitelé** se vztahuje na zařízení v síti, kterým je pro komunikační účely přiřazeno číslo identifikující je v rámci konkrétní sítě – **[[IP adresa]]** (adresa internetového protokolu). IP adresa identifikuje hostitele i síť, ke které je připojen.

Příklad klientského softwaru: webový prohlížeč (Chrome, Firefox).

## Peer-to-peer

Klientský a serverový software obvykle běží na oddělených počítačích, ale jeden počítač může plnit obě role současně. V malých firmách a domácnostech mnoho počítačů funguje jako servery i klienti – to je **[[peer-to-peer]] síť**.

**Výhody:**
- Snadné nastavení
- Méně složité
- Nižší náklady – nejsou potřeba síťová zařízení a dedikované servery
- Vhodné pro jednoduché úkoly (přenos souborů, sdílení tiskáren)

**Nevýhody:**
- Žádná centralizovaná správa
- Není tak bezpečné
- Není škálovatelné
- Všechna zařízení fungují jako klienti i servery, což může zpomalit jejich výkon

## Koncová zařízení

Nejznámější síťová zařízení. Každé má v síti adresu pro odlišení od ostatních. Když koncové zařízení zahájí komunikaci, použije adresu cílového zařízení k určení, kam zprávu doručit.

Koncové zařízení je buď zdrojem, nebo cílem zprávy přenášené po síti.

## Zprostředkující zařízení

Připojují jednotlivá koncová zařízení k síti a mohou propojit více sítí ([[switch]], [[router]], [[AP]]). Poskytují konektivitu a zajišťují tok dat v síti.

Používají adresu cílového koncového zařízení spolu s informacemi o síťových propojeních k určení cesty, kterou by zprávy měly procházet sítí.

## Síťová média

Média poskytují kanál, kterým zpráva putuje od zdroje k cíli. Moderní sítě používají tři typy médií:

- **Kovové dráty v kabelech** ([[UTP]], [[STP kabel|STP]]) – data kódována do elektrických impulsů.
- **Skleněná nebo plastová vlákna** ([[optické vlákno|optický kabel]]) – data kódována do světelných pulzů.
- **Bezdrátový přenos** ([[WLAN]]) – data kódována modulací specifických frekvencí elektromagnetických vln.
