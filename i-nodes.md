# I-NODES
# Symbolické linky

Symbolický link je speciální typ souboru, který slouží jako pokročilý odkaz nebo „zkratka“ k jinému souboru či adresáři v operačním systému.

## Klíčové vlastnosti
* **Ukazatel cesty:** Neobsahuje kopii dat původního souboru, ale pouze textovou informaci o tom, kde se cíl nachází.
* **Transparentnost:** Většina aplikací se symlinkem pracuje stejně jako se skutečným souborem/složkou.
* **Flexibilita:** Může odkazovat na soubory i složky napříč různými diskovými oddíly.
* **Nezávislost:** Smazáním linku se nesmaže původní soubor. Smazáním původního souboru se však link stane nefunkčním (**broken link**).

---

## Rozdíl: Symlink vs. Hard Link



| Vlastnost | Symbolický link | Pevný odkaz |
| :--- | :--- | :--- |
| **Co to je?** | Cesta k souboru (zkratka). | Další jméno pro stejná data na disku. |
| **Složky** | Lze vytvořit pro složky. | Většinou pouze pro soubory. |
| **Napříč disky** | Ano, funguje mezi oddíly/disky. | Ne, musí být na stejném oddílu. |
| **Po smazání zdroje** | Nefunkční (mrtvý odkaz). | Data zůstávají přístupná. |

---

## Praktické využití
1. **Správa verzí:** Odkaz `python` ukazuje na `python3.12`. Při aktualizaci jen změníte cíl linku.
2. **Úspora místa:** Místo kopírování velkých dat vytvoříte jen lehké odkazy.
3. **Synchronizace:** Mapování složek z různých částí disku do jedné složky pro cloud (např. Dropbox).

---

## Jak vytvořit symlink

### Linux a macOS (Terminál)
```bash
# ln -s [CÍL] [NÁZEV_LINKU]
ln -s /cesta/k/originalu /cesta/k/novemu/linku
```

# Mazání pevných linků
