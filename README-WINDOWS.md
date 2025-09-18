## Windows
### Přehled
Primární vývojová platforma. Projekt je nakonfigurován pro Microsoft Visual Studio 2022 (C++ workload). Všechny potřebné 3rd‑party knihovny, utility a data jsou součástí repozitáře.

### Požadavky
- Podpora OpenGL 4.x v ovladačích GPU
- Microsoft Visual Studio 2022 (Desktop development with C++)

#### Doporučené mapování přípon (***Tools → Options → Text Editor → File Extension***)
| Extension | Editor               |
|-----------|----------------------|
| glsl	    | Microsoft Visual C++ |
| mtl       | XML (Text) Editor    |
| tpp       | Microsoft Visual C++ |

### Klonování
1. Otevřít VS → ***Clone a repository*** → URL `https://github.com/wilhelmstoritz/zpg-projekt`
2. Otevřít řešení: `src/ZPGproject.sln`

> [!NOTE]
> Pro rychlejší první build lze dočasně unloadnout všechny projekty ve složce _`examples`_ (pravé tlačítko → ***Unload Projects in Solution Folder***).

### Build
Připraveny všechny konfigurace: `Debug|Win32`, `Debug|x64`, `Release|Win32`, `Release|x64`.

> [!TIP]
> Doporučeno `Debug|Win32` pro konzistenci binárek a typů.

### Spuštění
1. Nastavte startup projekt (např. `launcher`).
2. Build (Ctrl+Shift+B)
3. Spusťte (F5 / Ctrl+F5)

> [!NOTE]
Použita aktuální verze SOIL zkompilovaná ze zdrojových kódů. Původní varianta z tutoriálů je dostupná jako `3rd/soil.zpgdefault/`.

> [!CAUTION]
> Některé dodané knihovny (např. GLFW) nemusí být sestavené s runtime volbou `/MD`, což může vést k chybám při `Release` buildu. V případě potřeby přeložte vlastní binárky s konzistentními přepínači.
