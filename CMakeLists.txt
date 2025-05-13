cmake_minimum_required(VERSION 3.16)
project(port)



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
