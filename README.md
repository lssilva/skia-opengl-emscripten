# TODO
Shrink skia size
see https://github.com/skui-org/skia/blob/m74/CMakeLists.txt

### Clone with --recursive

```
sudo -E apt-get update
sudo -E apt-get install git build-essential wget
sudo -E apt-get install build-essential --reinstall
git clone --recursive {repourl_here}
```

### Ubuntu - Build and install CMake manually (recommended)
Uninstall any previous version (if needed):
```
sudo apt remove cmake
sudo apt purge --auto-remove cmake
```

Download, build and install the desired version from the terminal (you can check for the available versions at [the official CMake webpage](https://cmake.org/download/)).
You should set the CMAKE_VERSION and CMAKE_BUILD variables as needed:
```
export CMAKE_VERSION=3.11
export CMAKE_BUILD=3
mkdir -p ~/3rdparty
cd ~/3rdparty
wget https://cmake.org/files/v$CMAKE_VERSION/cmake-$CMAKE_VERSION.$CMAKE_BUILD.tar.gz
tar -xvzf cmake-$CMAKE_VERSION.$CMAKE_BUILD.tar.gz
rm cmake-$CMAKE_VERSION.$CMAKE_BUILD.tar.gz
cd cmake-$CMAKE_VERSION.$CMAKE_BUILD
./bootstrap
make -j4
sudo make install
```

### WASM

Download, install & configure emscripten as per your environment requires:

http://kripken.github.io/emscripten-site/docs/getting_started/downloads.html

### Build & clone deps with --init --recursive

```
git submodule update --init --recursive
```

```
# see http://commondatastorage.googleapis.com/chrome-infra-docs/flat/depot_tools/docs/html/depot_tools_tutorial.html#_setting_up
ls ${PWD}/thirdparty/depot_tools
export PATH="${PWD}/thirdparty/depot_tools:${PATH}"
```

Used deps:

> https://github.com/nigels-com/glew.git
```
# see https://github.com/nigels-com/glew#linux-and-mac
sudo -E apt-get install build-essential libxmu-dev libxi-dev libgl-dev --reinstall
sudo -E apt install libegl1-mesa-dev --reinstall
cd thirdparty/glew
cd auto
make

cd ../build
cmake ./cmake
cmake --build . -- -j4

sudo make install
```
> https://github.com/spurious/SDL-mirror.git
```
# see https://wiki.libsdl.org/Installation
cd thirdparty/SDL2
mkdir build
cd build
cmake ..
cmake --build . -- -j4
sudo make install
# NOTE You can even specify a custom path to find the SDL2, SDL2_net, ...
# see https://stackoverflow.com/a/55075667
```
> https://github.com/davidsiaw/SDL2_ttf
```
# see https://www.libsdl.org/projects/SDL_ttf/
# see https://www.libsdl.org/projects/SDL_ttf/docs/SDL_ttf_2.html
sudo apt-get install automake build-essential xorg-dev libudev-dev libts-dev libgl1-mesa-dev libglu1-mesa-dev libasound2-dev libpulse-dev libopenal-dev libogg-dev libvorbis-dev libaudiofile-dev libpng-dev libfreetype6-dev libusb-dev libdbus-1-dev zlib1g-dev libdirectfb-dev
sh autogen.sh
chmod +x configure
./configure
make
sudo make install
```
> https://github.com/aminosbh/sdl2-cmake-modules
```
# see https://stackoverflow.com/a/55075667
```
> https://skia.googlesource.com/skia.git
```
## clang
wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key --no-check-certificate | sudo apt-key add -
sudo apt-add-repository "deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-5.0 main"
sudo apt-add-repository "deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-6.0 main"
sudo apt-add-repository "deb http://apt.llvm.org/bionic/ llvm-toolchain-bionic-7 main"
sudo apt-add-repository "deb http://apt.llvm.org/bionic/ llvm-toolchain-bionic-8 main"
sudo -E apt-get update
sudo -E apt-get install build-essential
sudo -E apt-get install clang-6.0 python-lldb-6.0 lldb-6.0 lld-6.0 llvm-6.0-dev
sudo -E apt-get install clang-tools-6.0
sudo -E apt-get install libclang-common-6.0-dev libclang1-6.0 libclang-6.0-dev
sudo -E apt-get install libc++abi-dev libc++-dev
sudo apt-get install ninja-build libfreetype6-dev
sudo -E apt-get install libicu-dev libjpeg-dev libicu-dev libwebp-dev -y
# install icu https://stackoverflow.com/a/41314630
# harfbuzz
sudo apt-get install autoconf automake libtool pkg-config ragel gtk-doc-tools
git clone https://github.com/harfbuzz/harfbuzz.git
cd harfbuzz
./autogen.sh
./configure
make && sudo make install
# see https://github.com/google/skia/blob/master/site/user/build.md
# see https://github.com/google/skia/blob/master/modules/pathkit/README.md
ls ${PWD}/thirdparty/depot_tools
export PATH="${PWD}/thirdparty/depot_tools:${PATH}"
cd thirdparty/skia
tools/git-sync-deps
```

### Compile example on Linux

```
sh tools/build_linux.sh
```

### Run example on HTML5 platform (needs '--emrun' cxx flag)

```
emrun build-emscripten/index.html
```
