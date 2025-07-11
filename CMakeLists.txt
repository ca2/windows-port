cmake_minimum_required(VERSION 3.16)
project(port)


add_subdirectory(base/zlib)


if(${WIN32} OR ${ANDROID})
    add_subdirectory(base/sqlite)
endif()


if(${INCLUDE_FREETYPE} OR ${INCLUDE_FREEIMAGE} OR ${INCLUDE_IMAGING_FREEIMAGE})
    add_subdirectory(imaging/png)
endif()


if(${INCLUDE_FREEIMAGE} OR ${INCLUDE_IMAGING_FREEIMAGE})

    add_subdirectory(imaging/jpeg)
    add_subdirectory(imaging/jxr)
    add_subdirectory(imaging/openexr)
    add_subdirectory(imaging/openjpeg)
    add_subdirectory(imaging/rawlite)
    add_subdirectory(imaging/tiff4)
    add_subdirectory(imaging/webp)
    add_subdirectory(imaging/freeimage)


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