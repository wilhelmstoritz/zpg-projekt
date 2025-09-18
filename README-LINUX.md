## Linux
Testované distribuce: Fedora 41, Ubuntu 24.04.1 LTS.

> [!CAUTION]
> Wayland není podporován (omezení GLEW knihovny); **je nutné použít X11**.

### Požadavky
- GCC / Clang
- CMake + make
- OpenGL + X11 dev knihovny
- FFmpeg (volitelně pro záznam)
- Git (volitelně `gh`)

### Instalace balíčků
#### RHEL / Fedora
```
# development tools
sudo dnf -y update
sudo dnf -y install gcc-c++ cmake make

# libraries for OpenGL and related development; additional libraries and dependencies
sudo dnf -y install mesa-libGL-devel mesa-libEGL-devel libX11-devel libXrandr-devel libXinerama-devel libXcursor-devel libXi-devel
sudo dnf -y install glm-devel glfw-devel glew-devel assimp-devel SOIL-devel

# GitHub tools
sudo dnf -y install git gh

# FFmpeg
sudo dnf -y install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm # enable RPM Fusion repository
sudo dnf -y install ffmpeg --allowerasing
```

#### Debian / Ubuntu
```
# development tools
sudo apt update
sudo apt install -y g++ cmake make

# libraries for OpenGL and related development; additional libraries and dependencies
sudo apt install -y libgl1-mesa-dev libegl1-mesa-dev libx11-dev libxrandr-dev libxinerama-dev libxcursor-dev libxi-dev
sudo apt install -y libglm-dev libglfw3-dev libglew-dev libassimp-dev libsoil-dev

# GitHub tools
sudo apt install -y git gh

# FFmpeg
sudo apt install -y ffmpeg
```

### GitHub konfigurace (pokud není nastaveno)
```
gh auth login
git config --global user.email "you@mail.com"
git config --global user.name "your name"
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

> [!TIP]
> V případě problémů s OpenGL zkontrolujte, že běží X11 (např. `echo $XDG_SESSION_TYPE`).
