# Část 0: Proč začínat "nulovým" modulem

> Verze: 2026-10-03

## Základ, na kterém stojí všechno ostatní

Každá role popsaná v dalších modulech (řadič domény, souborový server...) běží na Windows Serveru, který musí mít od první minuty:

- **Jednoznačné jméno v síti** (hostname) — bez něj se server špatně identifikuje v Server Manageru, v DNS, v GPO cílení.
- **Stabilní síťovou adresu** — DHCP adresa serveru by se mohla časem změnit a rozbít všechno, co na ni ukazuje (DNS záznamy, klienti). Proto servery vždy dostávají **statickou** IP adresu, zatímco běžní klienti (Modul 2) adresu dostávají automaticky přes DHCP.
- **Bezpečný přístup administrátora** — v tomto projektu vždy přes vestavěný účet `Administrator`, nikdy přes personalizovaný účet vytvořený navíc (viz [[../00-pribeh-skoly|příběh školy]] — administrátor Jiří Pečlivý používá tento vestavěný účet, nemá vlastní pojmenovaný administrátorský účet).
- **Správnou lokalizaci** — jazyk rozhraní, časové pásmo a formáty data/času/měny. Špatně nastavené časové pásmo způsobí nesrovnalosti v časových razítkách logů, Kerberos autentizace (součást AD) je dokonce citlivá na přílišný časový rozdíl mezi serverem a klienty (výchozí tolerance je 5 minut) — proto se čas/časové pásmo řeší **hned na začátku**, ne až dodatečně.

## Windows Server Datacenter vs. Standard (kontext)

- **Standard**: běžná volba pro fyzické servery nebo servery s malým počtem virtuálních strojů (licenčně 2 VM na jednu licenci).
- **Datacenter**: neomezený počet virtualizovaných instancí na hostiteli a navíc obsahuje pokročilé funkce (např. Storage Spaces Direct, Shielded VMs), které Standard nemá.

Pro účely tohoto vzorového postupu používáme **Datacenter**, aby žádná ukázka (včetně těch pokročilejších v Modulu 6) nenarazila na licenční omezení edice — v reálném nasazení malé školy by ale často stačila i edice Standard.

## Server Core vs. Desktop Experience (kontext)

Windows Server lze nainstalovat i bez grafického rozhraní (**Server Core**) — má menší nároky na zdroje a menší útočnou plochu (méně součástí = méně záplat a zranitelností), ale spravuje se jen přes PowerShell nebo vzdáleně. V tomto projektu vždy volíme variantu **s Desktop Experience** (grafické rozhraní), protože cílem je naučit se pracovat i s GUI konzolemi (Server Manager, ADUC, DNS/DHCP Manager, Print Management) — v praxi je ale Server Core u produkčních řadičů domény a souborových serverů velmi běžná a doporučovaná volba.

## Windows 11 Education N a Microsoft účet (kontext pro PC1-WIN)

**Edice N** (dostupná pro Home/Pro/Education) neobsahuje přeinstalované mediální technologie (Windows Media Player, integrovanou kameru/hlasové nahrávání apod.) — je to varianta vzniklá kvůli antitrustovým rozhodnutím EU, funkčně jinak identická se standardní edicí; chybějící komponenty lze doinstalovat zvlášť, pokud jsou opravdu potřeba.

Na rozdíl od Windows Serveru **Windows 11 v OOBE aktivně vyžaduje přihlášení Microsoft účtem**, pokud stroj vidí síť — a nedovolí založit místní účet se jménem `Administrator` (to jméno patří vestavěnému účtu, který je ve výchozím stavu vypnutý). V praxi (firemní i školní nasazení) se tomu obchází buď souborem odpovědí (`autounattend.xml`, viz `cast2-powershell.md`), nebo run-time obejitím OOBE (odpojení sítě → "Continue with limited setup" → založení dočasného účtu → dodatečné povolení vestavěného `Administrator` účtu přes `net user administrator /active:yes`). Tento postup je zcela běžný při přípravě zlatých bitových kopií (golden image) pro velké nasazení, kde se stroje nemají hlásit pod osobními Microsoft účty.

## Odpovídá to i praxi Microsoftu

Windows Server samotný se dodává primárně v angličtině (produktová/instalační lokalizace); **český jazyk** se pak řeší přes **jazykové sady rozhraní (Language Packs)** a **regionální nastavení (Region)** — což je přesně to, co v tomto modulu nastavujeme: anglické rozhraní, ale české formáty a klávesnici. To je běžná kombinace i v komerčním prostředí, kde IT tým pracuje s anglickou terminologií, ale koncoví uživatelé (a systémové formáty data/měny) potřebují lokální zvyklosti.
