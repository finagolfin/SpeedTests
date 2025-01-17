# Speed Tests

When I learn a new programming language, I always implement the
Münchausen numbers problem in the given language. The problem is
simple but it includes a lot of computations, thus it gives an
idea of the execution speed of a language.

## Münchausen numbers

A [Münchausen number](https://en.wikipedia.org/wiki/Perfect_digit-to-digit_invariant)
is a number equal to the sum of its digits raised to each digit's power.

For instance, 3435 is a Münchausen number because
3<sup>3</sup>+4<sup>4</sup>+3<sup>3</sup>+5<sup>5</sup> = 3435.

0<sup>0</sup> is not well-defined, thus we'll consider 0<sup>0</sup>=0.
In this case there are four Münchausen numbers: 0, 1, 3435, and 438579088.

## Exercise

Write a program that finds all the Münchausen numbers. We know that the largest
Münchausen number is less than 440 million.

## Updates

Dates are in `yyyy-mm-dd` format.

**2024-01-21:** Perl was added.

**2023-04-02:** Toit and Codon were added.

## Implementations

In the implementations I tried to use the same (simple) algorithm in order
to make the comparisons as fair as possible.

All the tests were run on my home desktop machine (Intel Core i7-4771 CPU @ 3.50GHz with 8 CPU cores)
using Manjaro Linux. Execution times are wall-clock times and they are measured with
[hyperfine](https://github.com/sharkdp/hyperfine) (warmup runs: 2, benchmarked runs: 3).

The following implementations were received in the form of pull requests:

- Common LISP, Crystal, D, FASM, Fortran, Haskell, JavaScript, Lua, NASM, Pascal, Perl, Racket, Ruby,
Scheme, Toit, V, Zig

Thanks for the contributions!

If you know how to make something faster, let me know!

Languages are listed in alphabetical order.

The size of the EXE files can be further reduced with the command `strip -s`. If it's
applicable, then the stripped EXE size is also shown in the table.


### C

* gcc (GCC) 12.1.0
* clang version 14.0.6
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | stripped EXE (bytes) |
|-----|:---:|:---:|:---:|
| `gcc -O2 main.c -o main -lm` | 3.81 ± 0.005 | 20,680 | 14,416 |
| `clang -O2 main.c -o main -lm` | 2.629 ± 0.004 | 20,640 | 14,416 |

Notes:

* The switches `-O3` and `-Ofast` gave the same result as `-O2`, so
they were removed from the table.
* clang is better in this case

[see source](c)


### C#

* 7.0.102
* Benchmark date: 2023-02-06 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | -- |
|-----|:---:|:---:|:---:|
| `dotnet publish -o dist -c Release` | 5.873 ± 0.007 | 77,264 | -- |

Note: it's one second slower than Java.

[see source](cs)


### C++

* g++ (GCC) 12.1.0
* clang version 14.0.6
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | stripped EXE (bytes) |
|-----|:---:|:---:|:---:|
| `g++ -O2 --std=gnu++2a main.cpp -o main` | 3.864 ± 0.014 | 21,256 | 14,456 |
| `clang++ -O2 --std=c++2a main.cpp -o main` | 3.449 ± 0.001 | 21,200 | 14,456 |

Notes: clang is a bit better in this case.

[see source](cpp)


### Codon

* codon 0.15.5
* Benchmark date: 2023-04-02 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | stripped EXE (bytes) |
|-----|:---:|:---:|:---:|
| `codon build -release main.py` | 5.369 ± 0.006 | 28,400 | 26,864 |

Notes:

* Codon is a high-performance Python compiler that compiles Python code
  to native machine code without any runtime overhead.
* It's a bit faster than C#!
* The code is unchanged Python code. No type annotations are needed.

See https://github.com/exaloop/codon for more information about this compiler.

[see source](codon)

### Common LISP

* GNU CLISP 2.49.93+ (2018-02-18) (built on arojas [135.181.138.48])
* SBCL 2.2.5
* Benchmark date: 2022-09-02 [yyyy-mm-dd]

| Execution | Runtime (sec) | -- | -- |
|-----|:---:|:---:|:---:|
| `clisp -C main.cl` | 321.049 ± 0.484 | -- | -- |
| `sbcl --script main.cl` | 6.828 ± 0.003 | -- | -- |

Notes:

* `clisp` is very slow. Almost as slow as Python. And without the
`-C` switch, it's ten times slower.
* With `sbcl`, you can get excellent performance.

[see source](clisp)


### Crystal

* Crystal 1.5.0 (2022-07-21); LLVM: 14.0.6; Default target: x86_64-pc-linux-gnu
* Benchmark date: 2022-07-30 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | stripped EXE (bytes) |
|-----|:---:|:---:|:---:|
| `crystal build --release main.cr` | 3.624 ± 0.01 | 626,368 | 215,968 |

Notes:

* The runtime is excellent, comparable to C.
* The source code is almost identical to the Ruby source code.
* The build time in release mode is very slow. It was 12.8 seconds
on my machine.

See https://crystal-lang.org for more info about this language.

[see source](crystal)


### D

* DMD64 D Compiler v2.100.0
* LDC - the LLVM D compiler (1.29.0)
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | stripped EXE (bytes) |
|-----|:---:|:---:|:---:|
| `dmd -release -O main.d` | 9.987 ± 0.045 | 993,816 | 712,504 |
| `ldc2 -release -O main.d` | 3.089 ± 0.008 | 34,584 | 23,008 |

Notes:

* the runtime is comparable to C/C++
* the official compiler `dmd` is slow
* `ldc2` is the best in this case

[see source](d)


### Dart

* Dart SDK version: 2.17.6 (stable) (Tue Jul 12 12:54:37 2022 +0200) on "linux_x64"
* Node.js v18.6.0
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Execution | Runtime (sec) | compiled / transpiled output size (bytes) | -- |
|-----|:---:|:---:|:---:|
| `dart main.dart` | 23.909 ± 0.581 | -- | -- |
| `dart compile js main.dart -O2 -m -o main.js && node main.js` | 10.509 ± 0.032 | 31,684 | -- |
| `dart compile exe main.dart -o main && ./main` | 8.377 ± 0.009 | 5,925,856 | -- |

(`*`): in the first case, the Dart code is executed as a script

Notes:

* If you execute it as a script (JIT), it's slow.
* If you compile to native code (AOT), it's fast (though slower than Java/C#).
* stripping damaged the EXE file

[see source](dart)


### Elixir

* Erlang/OTP 24 [erts-12.3] [source] [64-bit] [smp:8:8] [ds:8:8:10] [async-threads:1] [jit]; Elixir 1.13.2 (compiled with Erlang/OTP 24)
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Execution | Runtime (sec) | -- | -- |
|-----|:---:|:---:|:---:|
| `elixir main.exs` | 227.963 ± 0.543 | -- | -- |
| `elixirc munchausen.ex && elixir caller.exs` | 217.528 ± 0.762 | -- | -- |

Notes:

* Elixir doesn't excel in CPU-intensive tasks.
* In the second case, the modules were compiled to `.beam` files. However, it
  didn't make the program much faster. The difference is very small.

[see source](elixir)


### FASM

* flat assembler  version 1.73.30
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | stripped EXE (bytes) |
|-----|:---:|:---:|:---:|
| `# FASM x64, see v1 in Makefile` | 15.792 ± 0.018 | 532 | 532 |
| `# FASM x86, see v2 in Makefile` | 15.207 ± 0.023 | 444 | 444 |

Note: no difference between the 32-bit and 64-bit versions.

See https://en.wikipedia.org/wiki/FASM for more info about FASM.

[see source](fasm)


### Fortran

* GNU Fortran (GCC) 12.1.0
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | stripped EXE (bytes) |
|-----|:---:|:---:|:---:|
| `gfortran -O2 main.f08 -o main` | 3.884 ± 0.054 | 21,016 | 14,456 |

Note: its speed is comparable to C.

[see source](fortran)


### Go

* go version go1.20 linux/amd64
* Benchmark date: 2023-02-04 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | stripped EXE (bytes) |
|-----|:---:|:---:|:---:|
| `go build -o main` | 4.366 ± 0.11 | 1,852,075 | 1,229,976 |

Notes:

* The speed is between C and Java (slower than C, faster than Java)
* The EXE is quite big (1.8 MB).

[see source](go)


### Haskell

* The Glorious Glasgow Haskell Compilation System, version 8.10.7
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | stripped EXE (bytes) |
|-----|:---:|:---:|:---:|
| `# basic, see v1 in Makefile` | 93.816 ± 0.043 | 3,175,704 | 754,008 |
| `# optimized, see v2 in Makefile` | 3.517 ± 0.009 | 6,324,936 | 3,183,648 |

Notes:

* The performance of the optimized version is comparable to C.
* However, when you compile the optimized version for the first time,
the compilation is very slow.

[see source](haskell)


### Java

* openjdk version "11.0.15" 2022-04-19
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Execution | Runtime (sec) | Binary size (bytes) | -- |
|-----|:---:|:---:|:---:|
| `javac Main.java && java Main` | 5.099 ± 0.018 | 1,027 | -- |

(`*`): the binary size is the size of the `.class` file

Note: very good performance.

[see source](java)


### JavaScript

* Node.js v18.6.0
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Execution | Runtime (sec) | -- | -- |
|-----|:---:|:---:|:---:|
| `node main.js` | 17.731 ± 0.015 | -- | -- |

[see source](javascript)


### Julia

* julia version 1.7.3
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Execution | Runtime (sec) | -- | -- |
|-----|:---:|:---:|:---:|
| `julia --startup=no main.jl` | 3.649 ± 0.009 | -- | -- |

Note: excellent performance, almost like C.

See https://julialang.org for more info about this language.

[see source](julia)


### Kotlin

* Kotlin version 1.6.20-release-275 (JRE 11.0.15+10)
* openjdk version "11.0.15" 2022-04-19
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Execution | Runtime (sec) | JAR size (bytes) | -- |
|-----|:---:|:---:|:---:|
| `kotlinc main.kt -include-runtime -d main.jar && java -jar main.jar` | 4.905 ± 0.011 | 4,588,993 | -- |

Note: same performance as Java.

[see source](kotlin)


### Lua

* Lua 5.4.4  Copyright (C) 1994-2022 Lua.org, PUC-Rio
* LuaJIT 2.1.0-beta3 -- Copyright (C) 2005-2022 Mike Pall. https://luajit.org/
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Compilation | Runtime (sec) | -- | -- |
|-----|:---:|:---:|:---:|
| `lua main.lua` | 118.23 ± 1.834 | -- | -- |
| `luajit main.lua` | 19.694 ± 0.009 | -- | -- |

Notes:

* LuaJIT is a Just-In-Time Compiler for Lua.
The language evolved and it contains an integer division operator (`//`), but LuaJIT
doesn't understand it.
* The Lua code ran much faster than the Python 3 (CPython) code.
* LuaJIT is fast. Its performance is similar to PyPy3 (even a little bit faster).

[see source](lua)


### NASM

* NASM version 2.15.05 compiled on Sep 24 2020
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | stripped EXE (bytes) |
|-----|:---:|:---:|:---:|
| `# NASM x86, see v2 in Makefile` | 15.19 ± 0.012 | 9,228 | 8,428 |
| `# NASM x64, see v1 in Makefile` | 15.186 ± 0.034 | 9,656 | 8,552 |

Note: no difference between the 32-bit and 64-bit versions.

See https://en.wikipedia.org/wiki/Netwide_Assembler for more info about NASM.

[see source](nasm)


### Nim Tests #1

* Nim Compiler Version 1.6.6 [Linux: amd64]
* gcc (GCC) 12.1.0
* clang version 14.0.6
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | stripped EXE (bytes) |
|-----|:---:|:---:|:---:|
| `nim c -d:release main.nim` | 4.638 ± 0.006 | 96,904 | 80,152 |
| `nim c -d:release --gc:orc main.nim` | 4.155 ± 0.049 | 73,000 | 59,568 |
| `nim c -d:release --gc:arc main.nim` | 4.124 ± 0.013 | 59,776 | 47,272 |
| `nim c --cc:clang -d:release main.nim` | 3.848 ± 0.006 | 80,608 | 63,752 |
| `nim c -d:danger --gc:orc main.nim` | 3.731 ± 0.01 | 59,120 | 47,280 |
| `nim c -d:danger --gc:arc main.nim` | 3.73 ± 0.008 | 50,120 | 39,080 |
| `nim c -d:danger main.nim` | 3.689 ± 0.002 | 91,656 | 76,056 |
| `nim c --cc:clang -d:release --gc:orc main.nim` | 3.611 ± 0.005 | 60,936 | 47,296 |
| `nim c --cc:clang -d:release --gc:arc main.nim` | 3.607 ± 0.004 | 51,712 | 39,096 |
| `nim c --cc:clang -d:danger --gc:orc main.nim` | 3.355 ± 0.011 | 46,968 | 35,008 |
| `nim c --cc:clang -d:danger --gc:arc main.nim` | 3.347 ± 0.001 | 42,104 | 30,904 |
| `nim c --cc:clang -d:danger main.nim` | 3.261 ± 0.006 | 67,144 | 51,464 |

(`*`): if `--cc:clang` is missing, then the default `gcc` was used

Notes:

* excellent performance, comparable to C
* in this case, clang gave better results than gcc
* danger mode gave a very little performance boost (with clang)
* The new garbage collectors (ARC and ORC) perform better than
the default garbage collector (with clang). The difference between
ARC and ORC is very little. If you have cyclic references, ORC is
the suggested garbage collector. Since the difference is so small,
and ORC is more general, maybe it's better to use ORC.
* To sum up, `--cc:clang -d:release --gc:orc` seems safe and fast.

[see source](nim)


### Nim Tests #2

* Nim Compiler Version 1.6.6 [Linux: amd64]
* gcc (GCC) 12.1.0
* clang version 14.0.6
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | stripped EXE (bytes) |
|-----|:---:|:---:|:---:|
| `# using int32, see v3 in Makefile` | 3.759 ± 0.003 | 60,936 | 47,296 |
| `# using int64, see v2 in Makefile` | 3.644 ± 0.03 | 60,936 | 47,296 |
| `# using int, see v1 in Makefile` | 3.639 ± 0.021 | 60,936 | 47,296 |
| `# using uint64, see v5 in Makefile` | 3.581 ± 0.013 | 60,984 | 47,296 |
| `# using uint32, see v4 in Makefile` | 3.065 ± 0.028 | 60,984 | 47,296 |

Here, we used the compiler options `--cc:clang -d:release --gc:orc`
everywhere and tested the different integer data types.

Notes:

* In Nim, the size of `int` is platform-dependent, i.e. it's 64-bit long on
a 64 bit system. Thus, on a 64 bit system, there is no difference between
using int and int64 (that is, v1 and v2 are quivalent).
* There's almost no difference between int / int64 (signed) and uint64 (unsigned).
* int32 (v3) was slower than int64, and uint32 (v4) produced the best result

[see source](nim2)


### Odin

* odin version dev-2022-07:98ba4bee
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | stripped EXE (bytes) |
|-----|:---:|:---:|:---:|
| `odin build . -no-bounds-check -disable-assert -o:speed` | 5.715 ± 0.007 | 219,792 | 207,624 |

See https://odin-lang.org for more info about this language.

Note: good performance, though a bit slower than C.

[see source](odin)


### Pascal

* Free Pascal Compiler version 3.2.2 [2022/03/02] for x86_64
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | stripped EXE (bytes) |
|-----|:---:|:---:|:---:|
| `fpc -O3 main.pas` | 17.454 ± 0.02 | 531,024 | 531,024 |

Notes:

* Three times slower than Java.
* Strangely, `strip` didn't make the EXE any smaller.

[see source](pascal)


### Perl

* This is perl 5, version 38, subversion 1 (v5.38.1) built for x86_64-linux-thread-multi
* Benchmark date: 2024-01-21 [yyyy-mm-dd]

| Execution | Runtime (sec) | -- | -- |
|-----|:---:|:---:|:---:|
| `perl main.pl` | 492.494 ± 3.441 | -- | -- |

[see source](perl)

Notes:

* This is the slowest solution. It's even slower than Python.

### Python 3

* Python 3.10.5
* Python 3.8.13 (4b1398fe9d76ad762155d03684c2a153d230b2ef, Apr 02 2022, 15:38:25) [PyPy 7.3.9 with GCC 11.2.0]
* Benchmark date: 2022-08-12 [yyyy-mm-dd]

| Execution | Runtime (sec) | -- | -- |
|-----|:---:|:---:|:---:|
| `python3 main.py` | 333.659 ± 1.942 | -- | -- |
| `pypy3 main.py` | 21.127 ± 0.128 | -- | -- |

Notes:

* CPython was the slowest :(
* PyPy3 is fast and comparable to LuaJIT

[see source](python3)


### Python 3.11

* Python 3.11.0
* Benchmark date: 2022-10-27 [yyyy-mm-dd]

| Execution | Runtime (sec) | -- | -- |
|-----|:---:|:---:|:---:|
| `python3.11 main.py` | 287.453 ± 5.975 | -- | -- |

Notes:

* 14% faster than Python 3.10 (strangely, 3.11 beta was 22% faster)
* More info here: https://github.com/faster-cpython/ideas/blob/main/FasterCPythonDark.pdf

[see source](python311)


### Python 3 with mypyc

* Python 3.10.5
* mypy 0.971 (compiled: no)
* Benchmark date: 2022-08-12 [yyyy-mm-dd]

| Execution | Runtime (sec) | .so (bytes) | stripped .so (bytes) |
|-----|:---:|:---:|:---:|
| `mypyc main.py && ./start_v3.sh` | 80.481 ± 0.574 | 183,992 | 92,824 |

Notes:

* `mypyc` can compile a module. This way, the program can be 4 to 5 times faster.

[see source](python3_with_mypyc)


### Python 3 with Nim

* Python 3.10.5
* Nim Compiler Version 1.6.6 [Linux: amd64]
* Benchmark date: 2022-08-13 [yyyy-mm-dd]

| Execution | Runtime (sec) | -- | -- |
|-----|:---:|:---:|:---:|
| `./start_v1.sh` | 46.772 ± 0.203 | -- | -- |

Notes:

* When you start it for the first time, it'll compile the Nim code
  as a shared library. Thus the first run may be slower.
* The real work is done in Nim. The Nim code is compiled as a shared library.
  The Python code just calls a function implemented in Nim.

[see source](python3_with_nim)


### Python 3 with Rust

* Python 3.10.5
* rustc 1.62.1 (e092d0b6b 2022-07-16)
* Benchmark date: 2022-08-12 [yyyy-mm-dd]

| Compilation | Runtime (sec) | -- | -- |
|-----|:---:|:---:|:---:|
| `# see v1 in Makefile && ./start_v1.sh` | 40.263 ± 1.152 | -- | -- |

Notes:

* The real work is done in Rust. The Rust code is compiled as a shared library.
  The Python code just calls a function implemented in Rust.
* The Rust code uses [pyo3](https://docs.rs/pyo3).
  Compilation is done with [maturin](https://github.com/PyO3/maturin).

[see source](python3_with_rust)


### Racket

* Welcome to Racket v8.5 [cs].
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Execution | Runtime (sec) | -- | -- |
|-----|:---:|:---:|:---:|
| `racket main.rkt` | 105.218 ± 0.312 | -- | -- |

See https://racket-lang.org for more info about this language.

[see source](racket)


### Ruby

* ruby 3.0.4p208 (2022-04-12 revision 3fa771dded) [x86_64-linux]
* Benchmark date: 2022-07-30 [yyyy-mm-dd]

| Execution | Runtime (sec) | -- | -- |
|-----|:---:|:---:|:---:|
| `ruby main.rb` | 199.632 ± 3.2 | -- | -- |
| `ruby --jit main.rb` | 75.863 ± 1.174 | -- | -- |

Notes:

* much faster than Python 3.10
* When run in JIT mode, the performance is the same as Python's
mypyc variant (where mypyc compiles a module).
* PyPy3 is 3-4 times faster than the JIT mode.

[see source](ruby)


### Rust

* rustc 1.62.1 (e092d0b6b 2022-07-16)
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | stripped EXE (bytes) |
|-----|:---:|:---:|:---:|
| `cargo build --release` | 2.936 ± 0.078 | 3,839,048 | 317,752 |

Notes:

* excellent performance (comparable to C/C++)
* The EXE is very big (almost 4 MB). However, if you strip the EXE,
the size becomes acceptable.

[see source](rust)


### Scheme

* chez 9.5.8
* guile (GNU Guile) 2.2.7
* gambitc v4.9.4
* stalin 0.11
* Benchmark date: 2022-09-18 [yyyy-mm-dd]

| Execution | Runtime (sec) | EXE (bytes) | -- |
|-----|:---:|:---:|:---:|
| `guile -s main.scm` | 148.423 ± 1.773 | -- | -- |
| `chez --compile-imported-libraries --optimize-level 3 -q --script main.scm` | 69.826 ± 0.387 | -- | -- |
| `gambitc -:debug=pqQ0 -exe -cc-options '-O3' main.scm && ./main` | 21.718 ± 0.229 | 9,098,392 | -- |
| `stalin -architecture amd64 -s -On -Ot -Ob -Om -Or -dC -dH -dP\ && ./main` | 4.599 ± 0.017 | 25,472 | -- |
| `stalin -architecture amd64 -s -On -Ot -Ob -Om -Or -dC -dH -dP\ && ./main` | 4.012 ± 0.014 | 25,512 | -- |

Note: stalin's performance is close to C.

[see source](scheme)


### Toit

* Toit version: v2.0.0-alpha.74
* Benchmark date: 2023-04-02 [yyyy-mm-dd]

| Execution | Runtime (sec) | EXE (bytes) | -- |
|-----|:---:|:---:|:---:|
| `toit.run main.toit` | 120.263 ± 0.069 | -- | -- |
| `toit.compile -O2 -o main main.toit && ./main` | 118.63 ± 0.774 | 1,254,784 | 1,254,784 |

Notes:
* The runtime of `toit.run` and `toit.compile` is the same. I'm not sure,
  but I think `toit.run` compiles to a temp. folder and starts the program from there.
* `toit.compile` must produce a stripped EXE. Stripping the EXE explicitly didn't change
  the file size.

See https://toitlang.org for more info about this language.

[see source](toit)

### V

* V 0.3.0 82db1e4
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | stripped EXE (bytes) |
|-----|:---:|:---:|:---:|
| `v -prod main.v` | 4.056 ± 0.004 | 209,392 | 187,728 |
| `v -cc clang -prod main.v` | 3.936 ± 0.018 | 212,720 | 191,736 |

By default, it uses GCC.

Note: its speed is comparable to C.

See https://vlang.io for more info about this language.

[see source](v)


### Zig

* zig 0.9.1
* Benchmark date: 2022-07-28 [yyyy-mm-dd]

| Compilation | Runtime (sec) | EXE (bytes) | stripped EXE (bytes) |
|-----|:---:|:---:|:---:|
| `zig build-exe -OReleaseFast src/main.zig` | 3.047 ± 0.006 | 105,872 | 10,240 |

Notes:

* Excellent performance (comparable to C/C++).
* The size of the stripped exe is tiny, just 10 KB! If you want the smallest
EXE without writing assembly, Zig is the way.

See https://ziglang.org for more info about this language.

[see source](zig)
