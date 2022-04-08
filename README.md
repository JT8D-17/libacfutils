# libacfutils

Fork of [skiselkov](https://github.com/skiselkov)'s [libacfutils](https://github.com/skiselkov/libacfutils) repo streamlining the build process. Intended for use to build [librain from this forked repository](https://github.com/JT8D-17/librain) for Linux and Windows (via MingW).    
Please visit the [original repo](https://github.com/skiselkov/libacfutils)  for the original readme and data.

&nbsp;

**Note that this fork is intended for Arch Linux and derivatives (like Manjaro). Package names and installation locations on other distros will vary.    
No Mac support!**

&nbsp;

## Package Requirements

Standard Arch Linux packages that are required for building `libacfutils`:    
`base-devel`, `cmake`, `libtool`, `unzip`, `qt5-base`, `libxcursor`, `glu`, `libpulse`, `alsa-lib`, `mingw-w64-gcc`    
(List may be incomplete or too extensive.)

&nbsp;

## Changes

- Updated `cglm`, `geographiclib`,`ocr`, `openal-soft`, X-Plane `SDK` dependencies
- Prebuilt linux-64 and win-64 libraries for the `cairo`, `curl`, `freetype`, `glew`, `libiconv`, `libpng`, `libxml`, `lzma`, `opus`, `pcre2`, `shapelib`, `ssl`, `zlib` dependencies sourced from [libacfutils redist 0.32](https://github.com/skiselkov/libacfutils/releases/tag/v0.32) to minimize compilation time
- Added `GL_for_Windows` (from [X-TCAS](https://github.com/skiselkov/X-TCAS)), `soil` and some `mingw64` dependencies for building [librain](https://github.com/skiselkov/librain) from this fork
- Modified `build_deps.sh` to consider prebuilt dependencies, add build logging and deactivate building of `ocr` (which just doesn't work)
- Modified `pkg-config-deps` to reflect updated `openal-soft` dependency
- Added a routine calling `autoreconf -i "$SRCDIR"` for `libxml2` to `build_dep.common` (not used due to prbuilt dependencies)
- Modified `qmake/qmake.pro` to enable building for Linux and Windows
- Added `qmake/build-lin` compilation script and `qmake/qmake-lin.pro` file
- Added `qmake/fallback` folder containing old, prebuilt libraies from [libacfutils redist 0.32](https://github.com/skiselkov/libacfutils/releases/tag/v0.32) 
- Modified `.gitignore` to consider prebuilt dependencies

&nbsp;

## Build tips

- Build dependecies with `build-deps` first
- Check if the dependencies were built correctly by looking for fatal errors in `z_buildlog.txt` or alternatively by checking the `[module name]-linux-64` and `[module name]-win-64` subfolders, which should have a `lib` folder with an `.a` file and/or `dll.a` file in them somewhere. This indicates a good build.
- Build order matters. Check `build-deps` from line 65 down to see what gets built when.
- If a module did not build from `build-deps`, go into its subfolder and run `build-[module name]-deps`. This usually catches build errors for that module much better.
- When all modules are built, you can build `libacfutils`with `qmake/build-win-lin`

