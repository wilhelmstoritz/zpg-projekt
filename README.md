# ZPG Projekt
Semestrální projekt – Základy počítačové grafiky (OpenGL 4.x).

## Platformy
- [Windows](README-WINDOWS.md)
- [macOS](README-MACOS.md)
- [Linux](README-LINUX.md)

**Testováno:** Windows 11, macOS 14 Sonoma, Fedora 41, Ubuntu 24.04.1 LTS.

> [!CAUTION]
> `appcore/AppUtils` používá platformově specifické API: Windows (`windows.h` / `direct.h`), macOS/Linux (`limits.h` / `unistd.h`). Pro jiné platformy je nutná úprava.
>
> `gloo/Renderer` používá `localtime_s` (Windows) / `localtime_r` (macOS/Linux).

## Struktura repozitáře
| Cesta | Popis |
|-------|-------|
| `src/` | Hlavní projekt (MSVS solution / CMake) |
| `3rd/` | 3rd‑party knihovny a pomocné nástroje (GLM, GLFW, GLEW, Assimp, SOIL, FFmpeg…) |
| `3rd.src/` | Zdrojové kódy 3rd‑party knihoven |
| `blender.src/` | Blender zdrojové soubory |
| `ARCHIVE/` | Archiv původních materiálů (přednášky, cvičení) |

### Moduly (v `src/`)
| Složka | Popis |
|--------|-------|
| `examples/` | Samostatné demonstrační projekty (každý se kompiluje zvlášť) |
| `resources/` | Modely, textury, fonty, GLSL shadery (`resources/shaders.glsl/<id>/`) |
| `appcore/` | Společné utility a konfigurace |
| `gl3rd/` | Poskytnuté zdrojové kódy (např. `ShaderLoader`) |
| `gloo/` | Objektová a scénová vrstva (modely, scény, renderer) |
| `launcher/` | Spuštění aplikace a výběr scén |

> [!NOTE]
> Pro spuštění vybraného příkladu v MS Visual Studio nastavte projekt jako Startup (pravé tlačítko → Set as Startup Project).

## Požadavky na grafiku / shadery
OpenGL 4.x ovladače. Výchozí GLSL verze ve zdrojích: `#version 430` (kompatibilita s VM). Na moderním hardware lze přepnout na `#version 460`.

## Architektonické požadavky
| Požadavek | Implementace |
|-----------|--------------|
| Zapouzdření shader programu | `ShaderProgram` neposkytuje raw ID; správa interně |
| Loader | Povinné použití `gl3rd/ShaderLoader` |
| Návrhové vzory | Singleton, Observer (světla ↔ shadery), Composite, Factory |
| Třída `Drawable` | Zavedena dle zadání; část funkcí v `Model` |
| Zpětná kompatibilita | Nové změny nesmí znefunkčnit existující scény (zejména scéna 03) |

## Build a platformní poznámky
- Preferováno: Windows / MSVC `Debug|Win32` pro konzistenci typů (`size_t`).
- Linux: požadováno X11 (Wayland nepodporován GLEW).
- macOS: některé OpenGL funkce označeny jako deprecated – bez dopadu na projekt.

## Scény a ovládání
Aktivace scén: úprava inicializace v projektu `launcher`. „Main menu“ umožňuje přepínání.

**Základní ovládání:**
| Klávesa | Funkce |
|---------|--------|
| X | Přepnutí fullscreen |
| W | Přepnutí wireframe |
| + / - | Úprava tloušťky čar ve wireframe |
| ESC | Ukončení aplikace |
| Myš (PP tlačítko) | Strafe / kamera |
| Šipky | Pohyb (SHIFT = rychle) |
| F | Zap/Vyp „flashlight“ |

**Specifická scéna „dark magic woods:fireballs“:**
| Klávesa | Funkce |
|---------|--------|
| 1–4 | Volba typu projektilu (fire / ice / dark / mystic) |
| 0 | Deaktivace projektilu |

## Konfigurace
Veškerá konfigurace: `appcore/Config`. Minimalizovat hard‑coded hodnoty mimo tento modul.

## Záznam videa (FFmpeg)
Povolte:
```
Config::SYSTEM_XTRA_RENDER_PROCESSING = true;
```
Každá scéna → samostatný `output.TIMESTAMP.mp4` v pracovním adresáři.

> [!IMPORTANT]
> Neměňte velikost okna při záznamu. Výchozí 800×600 musí odpovídat parametrům FFmpeg (lze upravit v `gloo/Renderer`).

## Údržba a doporučení
- Relativní cesty pro přenositelnost.
- Automatizovat kopírování závislostí do výstupních složek.
- Preferovat `std::unique_ptr` / `std::shared_ptr`, `enum class`, GL typy (`GLint` apod.).
- Při změnách shaderů/dat aktualizovat starší scény.

## Mapování indexů
Indexy scén (01, 02, 05a/05b, 06…) odpovídají průběhu zadání; shadery: `resources/shaders.glsl/<index>/`.

---
Stručný technický přehled. Platformně specifické detaily viz samostatné README soubory.
