# Spim CPU

This repository houses the backend of the Spim simulator: a simulator for
the MIPS R2000 and R3000 processors, a rudimentary operating system, a
linker, a loader, a simple debugger, and an assembler for MIPS-I and MIPS32
assembly programs.

The simulator backend is implemented as a static C++ library (archive) with
a C API. Frontends can then invoke the functions supplied by the API to
operate the simulated processor.

Frontends are required to supply definitions for the variables and functions
declared in [`include/spim-cpu/spim.h`](include/spim-cpu/spim.h) at link time.

The original work by James R. Larus can be found at
[SourceForge](https://spimsimulator.sourceforge.net), where the codebase
is hosted in an
[SVN repository](https://svn.code.sf.net/p/spimsimulator/code/).

## Changes

- The codebase has been refactored; this repository has the backend.
  Unfortunately, there is no test suite; the original test suite requires the
  accompanying console frontend to work.

- The order of `#include`s no longer matters (yes, it did in the original
  codebase). `#include` guards have also been added to headers.

- The project has been transitioned to [CMake](https://cmake.org).

## Building the project

### Requirements

You will need:

- [CMake](https://cmake.org) version 3.10 or higher;

- a C++ compiler toolchain (e.g., [GCC](https://gcc.gnu.org),
  [Clang](https://llvm.org),
  [MSVC](https://visualstudio.microsoft.com/vs/features/cplusplus)); and

- recent versions of
  [Flex](https://en.wikipedia.org/wiki/Flex_(lexical_analyzer_generator)) and
  [Bison](https://en.wikipedia.org/wiki/GNU_Bison) installed. On Linux
  distributions and macOS, these should be available via the package manager.
  On Windows, you may try [MSYS2](https://www.msys2.org),
  [Chocolatey](https://chocolatey.org) or similar, or install
  [WinFlexBison](https://github.com/lexxmark/winflexbison) via the
  [Windows Package Manager](https://github.com/microsoft/winget-pkgs/pull/284202).

### Build workflow

Run the following commands from the project root:

```bash
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release  # Generate the buildsystem
cmake --build build --config Release --parallel # Build the project
```

The static library [`libspim-cpu.a`](build/libspim-cpu.a) will be created
in the [`build`](build) directory.

> [!TIP]
> CMake enjoys good IDE support. Your IDE may be able to configure and build
> the project at the click of a button!
