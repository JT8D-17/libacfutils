# libacfutils

Fork of [skiselkov](https://github.com/skiselkov)'s [libacfutils](https://github.com/skiselkov/libacfutils) repo fixing build errors on Arch Linux.

Please visit the [original repo](https://github.com/skiselkov/libacfutils)  for the original readme.

&nbsp;

### Compiler script changes

- Added build logging to `build_deps.sh`
- Added `autoreconf -i "$SRCDIR"` to `build_dep.common.sh`

&nbsp;

### Updated modules (source and build script)

- cairo
- geographiclib
- libiconv
- libxml2
- ocr
- openAL-soft
- shapelib
- zlib