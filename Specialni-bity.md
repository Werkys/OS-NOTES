# Speciální bity (SUID, SGID, Sticky-bit)

Kromě standardních devíti bitů oprávnění existují tři speciální bity, které mění chování programů a složek.

---

## 1. Set UID (SUID)
* **Význam:** Program se spustí s právy svého **vlastníka**, nikoliv toho, kdo jej spustil.
* **Použití:** Typicky u programů jako `passwd` (uživatel musí zapsat do `/etc/shadow`, kam běžně nemá přístup).
* **Nastavení:** `chmod u+s program`
* **Zobrazení v `ls -l`:** * `s` – SUID nastaven + právo spouštět (x)
    * `S` – SUID nastaven, ale chybí právo spouštět
* **Poznámka:** U skriptů (bash, Python) se z bezpečnostních důvodů většinou ignoruje.

## 2. Set GID (SGID)
* **Význam u programů:** Program běží s právy **skupiny** vlastnící soubor.
* **Význam u složek:** Nově vytvořené soubory/složky uvnitř dědí **vlastnickou skupinu** od nadřazené složky (namísto primární skupiny uživatele).
* **Nastavení:** `chmod g+s slozka`
* **Zobrazení v `ls -l`:** Písmeno `s` (nebo `S`) na pozici práv skupiny.

## 3. Sticky-bit
* **Význam:** Používá se pro sdílené adresáře (např. `/tmp`). Zajišťuje, že uživatel může smazat pouze ty soubory, kterých je **vlastníkem**.
* **Nastavení:** `chmod o+t adresar`
* **Zobrazení v `ls -l`:** Písmeno `t` (nebo `T`) na pozici práv ostatních.

---

## umask (Uživatelská maska)
Definuje výchozí práva pro nově vytvořené objekty. Hodnota umask se **odečítá** od základní masky.

### Základní masky:
* **Soubory:** `666` (rw-rw-rw-)
* **Adresáře:** `777` (rwxrwxrwx)

### Příklad výpočtu (umask 022):
| Typ | Základ | umask | Výsledek | Význam |
| :--- | :--- | :--- | :--- | :--- |
| **Soubor** | 666 | 022 | **644** | rw-r--r-- |
| **Adresář** | 777 | 022 | **755** | rwxr-xr-x |
