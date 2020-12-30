project(lua C)
cmake_minimum_required(VERSION 3.18)

# If the user didn't set the build type, tell them debugging may fail.
if(NOT(CMAKE_BUILD_TYPE))
  message(
    WARNING
    "Build type was not set.  To export debugging symbols, set the "
    "build type with `-DCMAKE_BUILD_TYPE=Debug`."
    )
  set(CMAKE_BUILD_TYPE "Debug")
endif(NOT(CMAKE_BUILD_TYPE))

set(Lua_TARGET_DIR  ${CMAKE_BINARY_DIR}/target/${CMAKE_BUILD_TYPE})

# Define output directories
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${Lua_TARGET_DIR})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${Lua_TARGET_DIR})
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${Lua_TARGET_DIR})

add_subdirectory(src)
