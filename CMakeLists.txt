cmake_minimum_required(VERSION 3.16)
project(port)


add_subdirectory(base/zlib)


if(INCLUDE_FREEIMAGE)

    add_subdirectory(imaging/jpeg)
    add_subdirectory(imaging/jxr)
    add_subdirectory(imaging/openexr)
    add_subdirectory(imaging/openjpeg)
    add_subdirectory(imaging/tiff4)
    add_subdirectory(imaging/freeimage)


endif()



if(INCLUDE_FREETYPE)

    set(FT_WITH_PNG_PORT png)

    add_subdirectory(imaging/png)

    add_subdirectory(graphics/freetype)

endif()



if(INCLUDE_ICONV)

    add_subdirectory(base/iconv)

endif()



if(INCLUDE_IDN)

    add_subdirectory(base/idn)

endif()


if(INCLUDE_AUDIO)

    add_subdirectory(base/id3lib)

endif()


if(INCLUDE_OPENGL)

    add_subdirectory(graphics3d/glad)

endif()
