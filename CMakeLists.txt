cmake_minimum_required(VERSION 3.16)
project(port)

set(ZLIB_INCLUDE_DIR "")


if(NOT ${USE_SYSTEM_ARCHIVE})

add_subdirectory(base/archive)

endif()

if(NOT ${USE_SYSTEM_PCRE})

add_subdirectory(base/pcre)

endif()

if(NOT ${USE_SYSTEM_ZLIB})

add_subdirectory(base/zlib)
# Keep the compatibility port's static adapter outside the third-party repository.
if(__REACTOS__ AND TARGET zlib AND NOT TARGET static_zlib)
    get_target_property(ca2_zlib_sources zlib SOURCES)
    add_library(static_zlib STATIC ${ca2_zlib_sources})
    file(MAKE_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}/static-zlib-config/zlib")
    file(WRITE "${CMAKE_CURRENT_BINARY_DIR}/static-zlib-config/zlib/config.h"
        "#pragma once\n#undef ZLIB_DLL\n#undef Z_HAVE_UNISTD_H\n#undef _LARGEFILE64_SOURCE\n")
    target_include_directories(static_zlib BEFORE PUBLIC "${CMAKE_CURRENT_BINARY_DIR}/static-zlib-config")
    target_include_directories(static_zlib BEFORE PUBLIC "$<TARGET_PROPERTY:zlib,INCLUDE_DIRECTORIES>")
    target_compile_definitions(static_zlib PRIVATE __REACTOS__ _WIN32_WINNT=0x0501 WINVER=0x0501)
endif()

endif()

if(${WIN32} OR ${ANDROID})
    add_subdirectory(base/sqlite)
endif()


if(${INCLUDE_FREETYPE} OR ${INCLUDE_FREEIMAGE} OR ${INCLUDE_IMAGING_FREEIMAGE})
    add_subdirectory(imaging/port_png)
endif()


if(${INCLUDE_FREEIMAGE} OR ${INCLUDE_IMAGING_FREEIMAGE})

    add_subdirectory(imaging/port_jpeg)
    add_subdirectory(imaging/port_jxr)
    add_subdirectory(imaging/port_openexr)
    add_subdirectory(imaging/port_openjpeg)
    add_subdirectory(imaging/port_rawlite)
    add_subdirectory(imaging/port_tiff4)
    add_subdirectory(imaging/port_webp)
    add_subdirectory(imaging/port_freeimage)


endif()


if(${INCLUDE_FREETYPE})

    set(FT_WITH_PNG_PORT png)

    add_subdirectory(graphics/freetype)

endif()


if(${INCLUDE_ICONV} OR NOT ${HAS_SYSTEM_UNAC} OR ${INCLUDE_IDN})

    add_subdirectory(base/iconv)

endif()


if(NOT ${HAS_SYSTEM_UNAC})

    add_subdirectory(base/unac)

endif()


if(${INCLUDE_IDN})

    add_subdirectory(base/idn)

endif()


if(${INCLUDE_AUDIO})

    add_subdirectory(base/id3lib)

endif()


if(${INCLUDE_OPENGL})

    add_subdirectory(graphics3d/glad)

endif()

add_subdirectory(graphics/pixman)
add_subdirectory(graphics/cairo)