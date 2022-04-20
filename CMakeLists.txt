cmake_minimum_required(VERSION 3.18) # your CMake version.

# do something for specifed platform
if (MSVC)
    message(WARNING "MSVC") 
endif()

if (UNIX)
    message(WARNING "UNIX") 
endif()

if (APPLE)
    message(WARNING "APPLE") 
endif()

# project name
project(cpproj C CXX CUDA)
include(CTest) # for unit test

# your options
option(BUILD_UNIT_TEST "Build unit test." OFF) # for unit test
option(BUILD_XXX "Build XXX." OFF)
option(USE_XXX "Use XXX." OFF)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
# for your cmake scrip
set(CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake" "${CMAKE_MODULE_PATH}")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# c and cpp version
set(CMAKE_C_STANDARD 99)
set(CMAKE_CXX_STANDARD 17)

# add compiler options for cpp compiler
# ref: https://cmake.org/cmake/help/latest/variable/CMAKE_LANG_COMPILER_ID.html
# note: add_compile_options works on all compiler
if (CMAKE_CXX_COMPILER_ID STREQUAL "MSVC")
    if ("${CMAKE_CXX_FLAGS}" MATCHES "/W[1-3]")
        string(REGEX REPLACE "/W[1-3]" "/W4" CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")
    else()
        string(APPEND CMAKE_CXX_FLAGS " /W4")
    endif()
    string(APPEND CMAKE_CXX_FLAGS " /MP /wd4819 /wd4505 /wd4100 /wd4127")
elseif (CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    string(APPEND CMAKE_CXX_FLAGS " -Wall -Wno-unknown-pragmas -Wextra")
elseif (CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
    string(APPEND CMAKE_CXX_FLAGS " -Wall -Wno-unknown-pragmas -Wextra")
endif()

add_subdirectory(lib)
add_subdirectory(app)