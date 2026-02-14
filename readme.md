# 🐀 C++26 Modules basic project setup

![C++](https://img.shields.io/badge/C++-00599C?style=flat&logo=cplusplus&logoColor=white) [![C++](https://img.shields.io/badge/C++-26-blueviolet)](https://isocpp.org/)

Template for a C++26 project with modules.

# Prerequisites

- `Clang++` 19+
- `CMake` 3.30+
- `Ninja` 1.13+

# Setting up a project

Base setup requires:

- `main.cpp` as the core of the program
- `CMakeLists.txt` that points to it, as well as allows for linking any other libraries and modules
- `.clangd` file that makes sure your LSP can actually index everything correctly

> Your LSP might struggle to understand all modules until you run `cmake` once and let it export the build information that it can then pick up.

Then to build do:

```bash
cmake -G Ninja -S . -B build \
      -DCMAKE_CXX_COMPILER=clang++ \
      -DCMAKE_EXPORT_COMPILE_COMMANDS=ON
cmake --build build
```

and run the resulting executable from the build folder:

```bash
./build/app
```

# Modules

As of `C++26` module support exists if you use bleeding edge compilers and build tools. 

In your module `.cppm` file simply do:

```cpp
export module myModule;

export int myFunction(){
    return 1;
}
```

and import the module in `main.cpp` like:

```cpp
import myModule;
```

after linking it up in `CMakeLists.txt`:

```cmake
target_sources(app
    PUBLIC FILE_SET CXX_MODULES FILES
        src/myModule.cppm
)
```

When mixing includes and imports it's best to place includes first like:

```cpp
#include <print>
#include <vector>
import myModule;
```

> The support for `import std;` to use the standard library as a module is still insanely bad and not worth the hassle, but for your own code file you no longer need to fight with headers and implementations using modules is worth to gain benefits of incremental compilation, and have a more mangeable codebase.
