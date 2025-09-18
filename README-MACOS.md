## macOS
### Přehled
Používá se **Homebrew** pro instalaci závislostí (instaluje také **Xcode Command Line Tools**). Testováno na macOS 14+.

### Požadavky
- Homebrew
- GCC / Clang
- CMake + make
- OpenGL + X11 dev knihovny
- FFmpeg (volitelně pro záznam)
- Git (volitelně `gh`)

### Instalace nástrojů a knihoven
```
# Homebrew; also installs Xcode Command Line Tools
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# development tools
brew install gcc cmake make
PATH="/usr/local/opt/make/libexec/gnubin:$PATH"

# libraries for OpenGL and related development; additional libraries and dependencies
brew install mesa libx11 libxrandr libxinerama libxcursor libxi
brew install glm glfw glew assimp

# GitHub tools
brew install git gh

# FFmpeg
brew install ffmpeg
```

### GitHub konfigurace (pokud není nastaveno)
```
gh auth login
git config --global user.email "you@mail.com"
git config --global user.name "your name"
```

### SOIL build (volitelné)
Použijte pouze pokud systémová varianta není dostupná.
```
mkdir -p ~/src && cd ~/src
git clone https://github.com/childhood/libSOIL.git
cd libSOIL && make && sudo make install
```

### Klonování a build projektu
```
mkdir -p ~/src && cd ~/src
git clone https://github.com/wilhelmstoritz/zpg-projekt
cd zpg-projekt/src
cmake ./
make -j
```

### Spuštění
```
cd build
./ZPGproject
```
Spouštět z adresáře s binárkou kvůli relativním cestám.
