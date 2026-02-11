# CMake version
cmake_minimum_required(VERSION 4.2.3)

# Project name
project(cpp26_syntax_rev CXX)

set(CMAKE_CXX_STANDARD 26)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Link executables - with modules just main
add_executable(app src/main.cpp)

# Modules go here
target_sources(app
    PUBLIC FILE_SET CXX_MODULES FILES
        src/functions.cppm
)
