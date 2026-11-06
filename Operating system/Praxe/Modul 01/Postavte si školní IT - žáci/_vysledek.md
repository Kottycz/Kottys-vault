# [Jak se pozná, že už to mám?]

> Verze: 2026-10-03

Souhrnná kontrola celého projektu. Podrobné ověření jednotlivých kroků najdete v `_vysledek.md` každého modulu — toto je "finální zkouška" celku.

### 1. Přihlášení a identita
Na **PC1-WIN** se úspěšně přihlásíte jako `eva.student@prijmeni.cyberschool.internal`, `lucie.student@prijmeni.cyberschool.internal`, `jana.teacher@prijmeni.cyberschool.internal` i `karel.zamestnanec@prijmeni.cyberschool.internal` (všechna přihlášení fungují na tomtéž počítači, se stejným heslem `Pa55w.rd`, bez lokálních účtů).

### 2. Síť
Klient **PC1-WIN** má síťovou kartu nastavenou na "Obtain an IP address automatically" a přesto má funkční IP adresu z rozsahu `192.168.200.0/24`, funkční bránu a DNS. Příkaz `nslookup srv2-fs.prijmeni.cyberschool.internal` spuštěný na **PC1-WIN** vrátí správnou IP adresu `192.168.200.20`.

### 3. Group Policy
Přihlášený žák (`eva.student`) nemá přístup ke Ovládacím panelům / nemůže změnit pozadí plochy (dle nastavené GPO). Přihlášený učitel (`jana.teacher`) má jiná oprávnění. Příkaz `gpresult /r` na klientovi ukazuje aplikované GPO odpovídající OU uživatele.

### 4. Storage a souborové služby
Po fyzickém odebrání jednoho disku ze storage poolu na SRV2-FS (simulace poruchy) zůstávají data na sdíleném svazku nadále dostupná bez ztráty dat. Uživatel `eva.student` vidí a může zapisovat do své domovské složky na `\\SRV2-FS\Data\Studenti\Informatika\eva.student`, ale nevidí domovské složky ostatních uživatelů ani obsah `Vedeni`/`THP`/cizí předmětové komise.

### 5. FTP
Uživatel se z **PC1-WIN** přes klienta **FileZilla** úspěšně připojí (přes FTPS) na `ftp.prijmeni.cyberschool.internal`, nahraje soubor do `Studenti\Odevzdavani` a stáhne soubor z `Ucitele\Podklady`, s oprávněními odpovídajícími jeho roli.

### 6. Tisk
Po přihlášení uživatele na libovolném klientovi se automaticky objeví tiskárna odpovídající jeho roli a oboru (`jana.teacher` → `Tiskarna-Sborovna`, `eva.student` → `Tiskarna-Ucebna-Informatiky`, `lucie.student` → `Tiskarna-Ucebna-Gymnazium`), bez ruční instalace. Testovací stránka se úspěšně vytiskne (případně simulovaně přes tiskový ovladač).

### 7. Odolnost a dokumentace
Dokumentace v Obsidian vaultu obsahuje pro každý modul `__zadani.md`, postup a `_vysledek.md` a někdo jiný než autor je podle ní schopen infrastrukturu znovu sestavit nebo obnovit ze snapshotu.
