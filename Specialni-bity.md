# Speciální bity (SUID, SGID, Sticky-bit) v Unixu

Kromě standardních devíti bitů oprávnění (rwx pro vlastníka, skupinu a ostatní) existují tři speciální bity, které upravují chování programů a složek.

---

## 1. Set UID (SUID)
* **Význam:** Program je spuštěn s právy **vlastníka programu**, nikoliv toho, kdo jej spustil.
* **Použití:** Např. `/usr/bin/passwd` – uživatel musí mít možnost zapsat své nové heslo do `/etc/shadow`, kam má přístup pouze root.
* **Nastavení:** `chmod u+s soubor`
* **Indikace v `ls -l`:** * `s` – SUID nastaven + právo spouštět (x)
    * `S` – SUID nastaven, ale chybí právo spouštět
* **Upozornění:** U interpretovaných skriptů (Python, Bash) se z bezpečnostních důvodů ignoruje.

## 2. Set GID (SGID)
* **U souborů:** Program běží s právy **skupiny**, která soubor vlastní.
* **U složek:** Nově vytvořené soubory/složky uvnitř **dědí vlastnickou skupinu** od nadřazené složky (nikoliv primární skupinu tvůrce).
* **Nastavení:** `chmod g+s slozka`
* **Indikace v `ls -l`:** Písmeno `s` (nebo `S`) na pozici práv skupiny.

## 3. Sticky-bit
* **Význam:** Používá se pro sdílené adresáře (např. `/tmp`). Zaručuje, že uživatel může smazat pouze ty soubory, kterých je **vlastníkem**.
* **Nastavení:** `chmod o+t adresar`
* **Indikace v `ls -l`:** Písmeno `t` (nebo `T`) na pozici práv ostatních.

---

## umask (Uživatelská maska)

Nastavuje výchozí oprávnění pro nově vytvořené soubory a adresáře. Hodnota umask se binárně "odečítá" od základní masky pomocí operace `AND NOT`.

### Základní masky (Full access)
* **Soubory:** `666` (rw-rw-rw-) – Soubory se standardně nevytvářejí jako spustitelné.
* **Adresáře:** `777` (rwxrwxrwx)

### Binární rozpis (Příklad: umask 022)

#### Soubory (Základ 666)
| Část | Vlastník (rw-) | Skupina (rw-) | Ostatní (rw-) | Číselně |
| :--- | :--- | :--- | :--- | :--- |
| **Základ (666)** | `110` | `110` | `110` | 666 |
| **Umask (022)** | `000` | `010` | `010` | 022 |
| **Výsledek** | `110` | `100` | `100` | **644** |

#### Adresáře (Základ 777)
| Část | Vlastník (rwx) | Skupina (rwx) | Ostatní (rwx) | Číselně |
| :--- | :--- | :--- | :--- | :--- |
| **Základ (777)** | `111` | `111` | `111` | 777 |
| **Umask (022)** | `000` | `010` | `010` | 022 |
| **Výsledek** | `111` | `101` | `101` | **755** |

---

## Přehled číselné reprezentace (Octal mode)

Pro příkaz `chmod` se speciální bity uvádějí jako čtvrtá (předřazená) číslice:
* **4** = SUID
* **2** = SGID
* **1** = Sticky-bit

**Příklad:** `chmod 4755 soubor` (Nastaví SUID + rwxr-xr-x).
