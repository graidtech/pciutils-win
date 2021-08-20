cmake_minimum_required(VERSION 3.2)

project(libpci
    LANGUAGES C
    VERSION 3.5.5
    DESCRIPTION "PCI library for Windows")

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} /D_AMD64_")

add_custom_target(
	copy_win32_config
	COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_SOURCE_DIR}/../win32/config.h ${CMAKE_SOURCE_DIR}
)

add_library(libpci STATIC
    init.c
    access.c
    generic.c
    dump.c
    names.c
    filter.c
    names-hash.c
    names-parse.c
    names-net.c
    names-cache.c
    names-hwdb.c
    params.c
    caps.c
    i386-ports.c
)

add_dependencies(libpci copy_win32_config)

set_target_properties(libpci PROPERTIES VERSION ${PROJECT_VERSION})
