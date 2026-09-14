
![](https://doc.qt.io/qtforpython-6/_downloads/779d6d7ce1d79d357985f063a86786f3/logo.png)

# Qt Builds

This workflow builds Qt binaries.

All modules except QtWebEngine are included. QtMultimedia has no ffmpeg backend


## Installation

### Use in Qt Creator

1. Extract the toolchain wherever you want to keep it
2. In Qt Creator, go to "Projects" tab
3. Press "Manage Kits"
4. Go to Kits->Qt Versions 
5. Press "Add"
6. Select qmake or qmake6 executable present in the toolchain folder previously extracted under the "bin" subfolder
7. Press "Apply"
8. Go to Kits->Kits 
9. Press "Add"
10. Under the "Compiler" selection, select the correct compiler for the downloaded toolchain
11. Under the "Qr Version" selection, select the previously created Qt version
12. If needed, compile other fields
13. Press "Apply"

### Use it in terminal
1. Extract the toolchain wherever you want to keep it
2. Add the "bin" subfolder to your PATH
3. Add the correct compiler to your PATH

## Platform notes


### All platforms
- Configuration summmaries for each platform and version are present in the release tab
- All modules are included.
- QtMultimedia has no ffmpeg backend

### Linux

- Builds are configured with:
    - Embedded libjpeg, libpng, pcre, zlib
    - System harfuzz and freetype, since they are needed in order to use fontconfig for system fonts

### Windows

##### MinGW
- The correct MinGW version must be installed to the system and configured in Qt Creator. The exact GCC version used for the build is written in `mingw_version.txt` inside the toolchain folder.
- The MinGW runtime (libgcc, libstdc++, winpthread) is linked statically into every Qt DLL, plugin and tool, so no Qt file imports `libwinpthread-1.dll`, `libstdc++-6.dll` or `libgcc_s_seh-1.dll` and it does not matter which MinGW runtime is found first in your `PATH`. Qt itself is still a shared (DLL) build.
- Your own application still links the MinGW runtime DLLs dynamically (unless you use the same linker flags), so it needs the `bin` folder of the MinGW version listed in `mingw_version.txt` in its `PATH` or next to the executable.
- If you get an error like *"The procedure entry point nanosleep64 could not be located in Qt6Core.dll"* when running your own application, an older `libwinpthread-1.dll` from another program (e.g. GStreamer, Inkscape, an older MinGW) comes first in your `PATH`. Put the toolchain `bin` folder (or your MinGW `bin` folder) before those entries, or run the application from Qt Creator, which does this automatically.

##### MSVC

###### X64
- In order to use QtNetwork and QtOpcUa, OpenSSL must be installed. to do so, run 
```
vcpkg install openssl:x64-windows-static-release
```

###### ARM64
- In order to use QtNetwork and QtOpcUa, OpenSSL must be installed. to do so, run 
```
vcpkg install openssl:arm64-windows-static-release
```
- ARM64 builds are currently untested

### MacOS
- Builds are currently untested


