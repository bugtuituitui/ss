<p align="center"><img src="https://brotli.org/brotli.svg" alt="Brotli" width="64"></p>

# SECURITY NOTE

Please consider updating brotli to version 1.0.9 (latest).

Version 1.0.9 contains a fix to "integer overflow" problem. This happens when "one-shot" decoding API is used (or input chunk for streaming API is not limited), input size (chunk size) is larger than 2GiB, and input contains uncompressed blocks. After the overflow happens, `memcpy` is invoked with a gigantic `num` value, that will likely cause the crash.

### Introduction

Brotli is a generic-purpose lossless compression algorithm that compresses data
using a combination of a modern variant of the LZ77 algorithm, Huffman coding
and 2nd order context modeling, with a compression ratio comparable to the best
currently available general-purpose compression methods. It is similar in speed
with deflate but offers more dense compression.

The specification of the Brotli Compressed Data Format is defined in [RFC 7932](https://tools.ietf.org/html/rfc7932).

Brotli is open-sourced under the MIT License, see the LICENSE file.

> **Please note:** brotli is a "stream" format; it does not contain
> meta-information, like checksums or uncompresssed data length. It is possible
> to modify "raw" ranges of the compressed stream and the decoder will not
> notice that.

Brotli mailing list:
https://groups.google.com/forum/#!forum/brotli

![GitHub Actions Build Status](https://github.com/google/brotli/actions/workflows/build_test.yml/badge.svg)
[![Fuzzing Status](https://oss-fuzz-build-logs.storage.googleapis.com/badges/brotli.svg)](https://oss-fuzz-build-logs.storage.googleapis.com/index.html#brotli)

### Build instructions

#### Vcpkg

You can download and install brotli using the [vcpkg](https://github.com/Microsoft/vcpkg/) dependency manager:

    git clone https://github.com/Microsoft/vcpkg.git
    cd vcpkg
    ./bootstrap-vcpkg.sh
    ./vcpkg integrate install
    ./vcpkg install brotli

The brotli port in vcpkg is kept up to date by Microsoft team members and community contributors. If the version is out of date, please [create an issue or pull request](https://github.com/Microsoft/vcpkg) on the vcpkg repository.

#### Bazel

See [Bazel](http://www.bazel.build/)

#### CMake

The basic commands to build and install brotli are:

    $ mkdir out && cd out
    $ cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=./installed ..
    $ cmake --build . --config Release --target install

You can use other [CMake](https://cmake.org/) configuration.

#### Python

To install the latest release of the Python module, run the following:

    $ pip install brotli

To install the tip-of-the-tree version, run:

    $ pip install --upgrade git+https://github.com/google/brotli

See the [Python readme](python/README.md) for more details on installing
from source, development, and testing.

### Benchmarks
* [Squash Compression Benchmark](https://quixdb.github.io/squash-benchmark/) / [Unstable Squash Compression Benchmark](https://quixdb.github.io/squash-benchmark/unstable/)
* [Large Text Compression Benchmark](http://mattmahoney.net/dc/text.html)
* [Lzturbo Benchmark](https://sites.google.com/site/powturbo/home/benchmark)

### Related projects
> **Disclaimer:** Brotli authors take no responsibility for the third party projects mentioned in this section.

Independent [decoder](https://github.com/madler/brotli) implementation by Mark Adler, based entirely on format specification.

JavaScript port of brotli [decoder](https://github.com/devongovett/brotli.js). Could be used directly via `npm install brotli`

Hand ported [decoder / encoder](https://github.com/dominikhlbg/BrotliHaxe) in haxe by Dominik Homberger. Output source code: JavaScript, PHP, Python, Java and C#

7Zip [plugin](https://github.com/mcmilk/7-Zip-Zstd)

Dart [native bindings](https://github.com/thosakwe/brotli)

Dart compression framework with [fast FFI-based Brotli implementation](https://pub.dev/documentation/es_compression/latest/brotli/brotli-library.html) with ready-to-use prebuilt binaries for Win/Linux/Mac
