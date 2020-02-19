Ankou Benchmark Sources
===

`sources/*.tar.xz` archives contain the source of the 24 program packages
with the same version used for the evaluation of "Ankou: Guiding Grey-box
Fuzzing towards Combinatorial Difference", ICSE 2020.
`seeds.tar.xf` contains the seeds used to initialize the fuzzing campaigns.

## Extracting the archives

```bash
git clone https://github.com/SoftSec-KAIST/Ankou-Benchmark
cd Ankou-Benchmark
tar xf seeds.tar.xz
cd sources
ls *.tar.xz | xargs -n1 tar xf
```

## Usage

Once extracted, each package can be compiled with `afl-gcc`. Most packages
can be compiled via `./configure; make; make install`. For example:
```bash
cd sources/cflow-1.6
CC=afl-gcc CXX=afl-g++ ./configure --prefix=`pwd`/build
make -j
make install
```

For some packages, using `cmake` is required. For example:
```bash
cd sources/exiv2-0.27.1-Source
mkdir build; cd build
cmake .. \
    -DCMAKE_INSTALL_PREFIX=./locals \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_C_COMPILER=afl-gcc -DCMAKE_CXX_COMPILER=afl-g++
make -j
make install
```

`libgxps-0.3.1` requires `meson` to compile.
