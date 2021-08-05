# libacfutils

Fork of [skiselkov](https://github.com/skiselkov)'s [libacfutils](https://github.com/skiselkov/libacfutils) repo fixing build errors on Arch Linux. Intended for use to build [librain from this forked repository](https://github.com/JT8D-17/librain) for Linux and Windows (via MingW).    
Please visit the [original repo](https://github.com/skiselkov/libacfutils)  for the original readme and data.

&nbsp;

**Note that this fork isintended for Arch Linux and any derived distro (like Manjaro). Package names and installation locations on other distros will vary.    
No Mac support, sorry!**

&nbsp;

## Package Requirements

The standard packages that are required for building `libacfutils`:    
`base-devel`, `cmake`, `libtool`, `unzip`, `qt5-base`, `libxcursor`, `glu`, `libpulse`, `alsa-lib`, `mingw-w64-gcc`    
(List may be incomplete or too extensive.)

For this fork, these AUR packages (mind their dependencies!):

- [mingw-w64-proj](https://aur.archlinux.org/packages/mingw-w64-proj/)
- [mingw-w64-freetype2](https://aur.archlinux.org/packages/mingw-w64-freetype2/)

(Hint: Add [the unofficial ownstuff repository](https://wiki.archlinux.org/title/unofficial_user_repositories#ownstuff) to pacman if you want to download binaries instead of having to compile everything.)




&nbsp;

## Changes

- Updated source packages for `cairo`, `geographiclib`, `libiconv`, `libxml2`, `ocr`, `openal-soft`, `shapelib`, `zlib`
- Added build logging to `build_deps.sh`
- Deactivated building `ocr` in `build_deps.sh` because it just did not work at all
- Added a routine calling `autoreconf -i "$SRCDIR"` for `libxml2` to `build_dep.common`
- Win64 `freetype2` now referenced from system (see package requirement above and `freetype/build_freetype_deps`)
- Enabled shared DLL build for win64 `libpng`
- Win64 `glew` now built regardless of "minimal" build script setting
- Win64 `proj`(for `shapelib`) now referenced from systen (see package requirement above and `shapelib/build_shapelib_deps`)
- Added more includes to `qmake\qmake.pro`
- Added `GL_for_Windows`folder from [X-TCAS](https://github.com/skiselkov/X-TCAS) as a safety dependency for building [librain](https://github.com/skiselkov/librain) from this fork


&nbsp;

## Build tips

- Build dependecies with `build-deps` first
- Check if the dependencies were built correctly by looking for fatal errors in `z_buildlog.txt` or alternatively by checking the `[module name]-linux-64` and `[module name]-win-64` subfolders, which should have a `lib` folder with an `.a` file and/or `dll.a` file in them somewhere. This indicates a good build.
- Build order matters. Check `build-deps` from line 65 down to see what gets built when.
- If a module did not build from `build-deps`, go into its subfolder and run `build-[module name]-deps`. This usually catches build errors for that module much better.
- When all modules are built, you can build `libacfutils`with `qmake/build-win-lin`

