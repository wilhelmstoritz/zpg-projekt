# ZPG projekt
### semestr 03 | Základy počítačové grafiky; projekt
Semestrální projekt; OpenGL 4.x.

## Platformy
- [Windows](README-WINDOWS.md)
- [macOS](README-MACOS.md)
- [Linux](README-LINUX.md)

> **Testováno:** Windows 11, macOS 14 Sonoma, Fedora 41, Ubuntu 24.04.1 LTS.

> [!CAUTION]
> `appcore/AppUtils` používá platformově specifické API: Windows (`windows.h` / `direct.h`), macOS/Linux (`limits.h` / `unistd.h`). Pro jiné platformy je nutná úprava.
>
> `gloo/Renderer` používá `localtime_s` (Windows) / `localtime_r` (macOS/Linux).

## Struktura repozitáře
| Adresář       | Co tam je                                                                                    |
|---------------|----------------------------------------------------------------------------------------------|
| `src`         | Vlastní projekt; MSVS solution root                                                          |
| `3rd`         | 3rd-party knihovny (GLM, GLFW, GLEW a další) a programy (FFmpeg) atd.                        |
| `3rd.src`     | Zdrojové kódy k 3rd-party knihovnám                                                          |
| `blender.src` | Zdrojové soubory pro Blender                                                                 |
| `ARCHIVE`     | Archiv všeho co jsme dostali k dispozici v původní podobě; **přednášky** + **cvičení** z LMS |

### Struktura projektu (moduly v `src/`)
| Knihovna/Složka  | Co tam je                                                               |
|------------------|-------------------------------------------------------------------------|
| dir: `examples`  | Jednotlivé ukázkové příklady co jsme dostali během tutoriálů            |
| dir: `resources` | Všechna ostatní data; modely, textury, fonty; **zdrojové kódy shaderů** |
|                  |                                                                         |
| `appcore`        | App core; sdílená knihovna nástrojů a utilit                            |
| `gl3rd`          | GL 3rd-party; dodané zdrojové kódy k zakomponování do projektu          |
| `gloo`           | GL object oriented; vlastní implementace projektu                       |
| `launcher`       | Launcher; vytváření scény                                               |

> [!NOTE]
> Pro spuštění vybraného příkladu nastavte v MS Visual Studiu projekt jako Startup (pravé tlačítko → ***Set as Startup Project***).

## Nějaké info co mi přijde důležité
> Pro spuštění je potřeba mít ovladače podporující OpenGL v4.x; na integrované kartě to (možná) pustíte ale rozhodně to nebude použitelné. Verze shaderů ve zdrojácích je nastavená na 4.30 (kompatibilita s VMWare VM), pro moderní HW nastavte na `#version 460 core`.

Projekt se dá psát na jakékoliv platformě; doporučuji se držet MSVS a Windows. **Je to jediná platforma kde použité knihovny fungují bez problémů!**; na většině moderních Linux distribucích a/nebo macOS jsou nějaká omezení (na Linuxu GLEW nepodporuje Wayland, na macOS jsou různé funkce z GL knihoven označeny jako _deprecated_ a nahrazeny Metal API...)

> [!NOTE]
> Doporučuji vše kompilovat pro `Debug|Win32` pro konzistenci binárek a typů (win32 `size_t` je `unsigned long` vs win64 `size_t` je `unsigned long long` apod.)

> [!TIP]
> - všude kde to dává smysl používejte (smart) pointery `std::unique/shared_ptr` místo `*ptr`; ušetří to dost času a nervů
> - hlídejte si typovou bezpečnost (`enum class` místo `enum`, `GLint` a obecně GL proměnné tam kde se očekávají apod.)

> [!NOTE]
> Vše ve zdrojácích s indexem (01, 02 .. 05a/05b, 06 apod.) souvisí s daným tutoriálem (scéna 03 "illuminated spheres" odpovídá tutoriálu 3 a používá zdrojové soubory k shaderům ve složce `resources/shaders.glsl/03/`). _Pozn: Přednášky a cvičení jsou očíslováné 1 - 10, tutoriálů bylo 6, proto číslování v kódu nemusí nutně korespondovat s číslem přednášky/cvičení které se daným tématem zabývá._
> Občas v kódu narazíte na zakomentovanou "implementaci něčeho" - většinou se jedná o nějaké řešení které bylo nahrazeno jinou verzí; měl by tam být aspoň nějaký základní komentář o co jde.

### Jak to používat
V _launcheru_ zakomentovat/povolit scény které chcete pustit. Každá scéna má k dispozici nějaké ovládání; viz. info v titulku okna.

> Všechny podporují:
>  - **X** pro přepínání celoobrazovkového (fullscreen) režimu,
>  - **W** pro přepínání vykreslování polygonů (wireframe) pro ladění (**+**/**-** toušťka čáry),
>  - **ESC** pro ukončení.

> Většina scén dále podporuje:
>  - pohyb pomocí **myši** (**pravé tlačítko** = strafe),
>  - pohyb pomocí **kurzorových kláves** (**SHIFT** = sprint),
>  - **F** pro vyp/zap baterky.

> Poslední scéna "dark magic woods:fireballs" pak navíc umožňuje hodit 'ohnivou kouli':
>  - **1-4** tradiční ohnivá / ledová / temná / mystická,
>  - **0** zhasnutí/ostranění.

#### Konfigurace
Veškerá konfigurace by měla být dostupná skrze `appcore/Config`; hardcoded by mělo být naprosté minimum věcí.

#### Nahrávání videa z výstupu
Občas se objeví požadavek na video z výstupu aplikace. Aby se zachytávání obrazovky/okna nemuselo řešit extra, je implementováno nahrávání obsahu okna pomocí FFmpeg. Stačí v `appcore/Config` nastavit
```Config::SYSTEM_XTRA_RENDER_PROCESSING = true;```

# 🍀 Good Luck!
