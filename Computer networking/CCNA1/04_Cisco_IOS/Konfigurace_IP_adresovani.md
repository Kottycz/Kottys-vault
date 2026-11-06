# Konfigurace IP adresování

**[[DHCP]]** (Dynamic Host Configuration Protocol) – dynamické přidělování [[IP adresa|IP adres]] (viz [[DORA]]).

## Konfigurace virtuálního rozhraní přepínače (SVI)

Pro konfiguraci rozhraní [[SVI]] na [[switch|přepínači]] se použije globální konfigurační příkaz:

```
interface vlan 1
```

[[VLAN]] 1 není skutečné fyzické rozhraní, ale virtuální.
