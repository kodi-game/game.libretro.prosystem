project(game.libretro.prosystem)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(Kodi REQUIRED)

include(ExternalProject)

if(CMAKE_BUILD_TYPE MATCHES Debug)
  set(LIBRETRO_DEBUG DEBUG=1)
endif()

if("${CORE_SYSTEM_NAME}" STREQUAL "windows")
  set(BUILD_COMMAND mingw32-make platform=win ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "linux")
  set(BUILD_COMMAND make ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "darwin")
  set(BUILD_COMMAND make platform=osx ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "ios")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "android")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "rbpi")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "freebsd")
# TODO
endif()

externalproject_add(prosystem
                    GIT_REPOSITORY https://github.com/libretro/prosystem-libretro
                    GIT_TAG d37def2
                    PREFIX prosystem
                    CONFIGURE_COMMAND ""
                    INSTALL_COMMAND ""
                    BUILD_COMMAND ${BUILD_COMMAND}
                    BUILD_IN_SOURCE 1)

set(PROSYSTEM_CUSTOM_BINARY ${PROJECT_BINARY_DIR}/prosystem/src/prosystem/prosystem_libretro${CMAKE_SHARED_LIBRARY_SUFFIX}
                            game.libretro.prosystem${CMAKE_SHARED_LIBRARY_SUFFIX} prosystem)

build_addon(game.libretro.prosystem PROSYSTEM DEPLIBS)
add_dependencies(game.libretro.prosystem prosystem)

include(CPack)
