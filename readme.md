# 🐀 C++26 Syntax Revision

![C++](https://img.shields.io/badge/C++-00599C?style=flat&logo=cplusplus&logoColor=white) [![C++](https://img.shields.io/badge/C++-26-blueviolet)](https://isocpp.org/)

Little syntax revision notes for C++26 and onwards.

# Prerequisites

- `Clang++` 18+
- `CMake` 4+
- `Ninja` 1.13+

# Setting up a project

Base setup requires:

- `main.cpp` as the core of the program
- `CMakeLists.txt` that points to it, as well as allows for linking any other libraries and modules
- `.clangd` file that makes sure your LSP can actually index everything correctly

Then to build do:

```bash
cmake -G Ninja -S . -B build \
      -DCMAKE_CXX_COMPILER=clang++ \
      -DCMAKE_EXPORT_COMPILE_COMMANDS=ON
cmake --build build
```

and run the resulting executable from the build folder.

# Modules

As of `C++26` module support exists if you use bleeding edge compilers and build tools. 

The support for `import std;` to use the standard library as a module is still insanely bad and not worth the hassle, but for your own code file you no longer need to fight with headers and implementations and can instead use modules!

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

after linking it up in `CMakeLists.txt`. 

When mixing includes and imports it's best to place includes first like:

```cpp
#include <print>
#include <vector>
import functions;
```
