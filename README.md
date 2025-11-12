# Vstup a výstup procesů

# 💡 Základy a procesy

Přesměrování vstupů je způsob komunikace mezi procesy.  
Filozofie Unixu říká, že programy mají být jednoduché – dělat jednu věc a dělat ji dobře.

Každý proces si můžeme představit jako **černou skříňku**, která má definované standardní komunikační kanály:

| Kanál                   | Popis                                   | Virtuální soubor |
|--------------------------|-----------------------------------------|------------------|
| **Standardní vstup**    | Za normálních okolností klávesnice.     | `/dev/stdin`     |
| **Standardní výstup**   | Za normálních okolností obrazovka.      | `/dev/stdout`    |
| **Standardní chybový výstup** | Za normálních okolností obrazovka. | `/dev/stderr`    |

Vstup a výstup programů lze navzájem propojit.

---

## 🔄 Varianty přesměrování (Redirection)

| Příkaz | Funkce | Detail |
|--------|---------|--------|
| `program > soubor` | Přesměrování standardního výstupu | Výstup programu se zapíše do souboru (přepíše stávající data). |
| `program >> soubor` | Připojení na konec souboru | Nová data se připojí na konec souboru. |
| `program 2> soubor` | Přesměrování chybového výstupu | Chybové hlášky se zapíší do zadaného souboru. |
| `program < soubor` | Přesměrování standardního vstupu | Program čte data ze souboru místo z klávesnice. |

---

## 🔗 Propojení programů (Roura / Pipe)

Propojení dvou procesů se provádí pomocí **roury** (`|`).

- Roura je nástroj pro komunikaci mezi procesy.  
- Při použití `program1 | program2`:
  - výstup `program1` se stane vstupem `program2`.  
- Tak lze vytvořit **kolonu příkazů** (*pipeline*), např.:
  ```bash
  ls | sort | head
