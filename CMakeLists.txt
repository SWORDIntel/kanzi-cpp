cmake_minimum_required(VERSION 3.10)
project(kanzi)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find source files
file(GLOB_RECURSE KANZI_SOURCES 
    src/*.cpp
    src/**/*.cpp
)

# Exclude main files
list(FILTER KANZI_SOURCES EXCLUDE REGEX ".*main\.cpp$")
list(FILTER KANZI_SOURCES EXCLUDE REGEX ".*app/.*\.cpp$")

# Create library
add_library(kanzi STATIC ${KANZI_SOURCES})

# Include directories
target_include_directories(kanzi PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
    $<INSTALL_INTERFACE:include>
)

# Compiler flags
target_compile_options(kanzi PRIVATE
    -O3
    -march=native
    -Wall
)
