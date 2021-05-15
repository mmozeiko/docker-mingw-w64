# mingw-w64

Builds [mingw-w64][] toolchain in docker for targeting 64-bit Windows from Ubuntu 18.04.

This docker image will contain following software built from source:

* [pkg-config][] v0.29.2
* [cmake][] v3.20.2
* [binutils][] v2.36.1
* [mingw-w64][] v8.0.0
* [gcc][] v11.1.0
* [nasm][] v2.15.05

Extra binaries:

* extra Ubuntu packages: `wget`, `patch`, `bison`, `flex`, `yasm`, `make`, `ninja`, `meson`, `zip`.
* [nvcc][] v11.3.0

Custom built binaries are installed into `/usr/local` prefix. [pkg-config][] will look for packages in `/mingw` prefix. `nvcc` is available in `/usr/local/cuda/bin` folder.

# Using

Execute following to run your shell script, makefile or other build script from current folder:

    docker run --rm -ti -v `pwd`:/mnt mmozeiko/mingw-w64 ./build.sh

For autotools builds add following arguments:

    --prefix=${MINGW} \
    --host=x86_64-w64-mingw32 \

For cmake builds add following arguments:

    -DCMAKE_SYSTEM_NAME=Windows \
    -DCMAKE_INSTALL_PREFIX=${MINGW} \
    -DCMAKE_FIND_ROOT_PATH=${MINGW} \
    -DCMAKE_FIND_ROOT_PATH_MODE_PROGRAM=NEVER \
    -DCMAKE_FIND_ROOT_PATH_MODE_LIBRARY=ONLY \
    -DCMAKE_FIND_ROOT_PATH_MODE_INCLUDE=ONLY \
    -DCMAKE_C_COMPILER=x86_64-w64-mingw32-gcc \
    -DCMAKE_CXX_COMPILER=x86_64-w64-mingw32-g++ \
    -DCMAKE_RC_COMPILER=x86_64-w64-mingw32-windres \

[pkg-config]: https://www.freedesktop.org/wiki/Software/pkg-config/
[cmake]: https://cmake.org/
[binutils]: https://www.gnu.org/software/binutils/
[mingw-w64]: https://mingw-w64.org/
[gcc]: https://gcc.gnu.org/
[nasm]: https://nasm.us/
[nvcc]: https://docs.nvidia.com/cuda/cuda-compiler-driver-nvcc/index.html
