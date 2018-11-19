cmake_minimum_required(VERSION 3.1)
project(game.libretro.prosystem)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

find_package(Kodi REQUIRED)
find_library(PROSYSTEM_LIB NAMES prosystem_libretro${CMAKE_SHARED_LIBRARY_SUFFIX} PATH_SUFFIXES libretro)

set(PROSYSTEM_CUSTOM_BINARY ${PROSYSTEM_LIB}
    ${PROJECT_NAME}${CMAKE_SHARED_LIBRARY_SUFFIX})

build_addon(${PROJECT_NAME} PROSYSTEM "")

include(CPack)
