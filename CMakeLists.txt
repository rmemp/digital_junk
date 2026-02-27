cmake_minimum_required(VERSION 3.25)

set(VERSION_MAJOR 0)
set(VERSION_MINOR 0)
set(VERSION_PATCH 0)
set(VERSION_TWEAK 0)

project(project
VERSION ${VERSION_MAJOR}.${VERSION_MINOR}.${VERSION_PATCH}.${VERSION_TWEAK}
LANGUAGES C CXX ASM_NASM
)


set(CMKAKE_CXX_STANDARD 26)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_C_STANDARD 23)
set(CMAKE_C_STANDARD_REQUIRED ON)



if(NOT (${CMAKE_BINARY_DIR} STREQUAL ${CMAKE_SOURCE_DIR}/build))
    message(${CMAKE_BINARY_DIR})
    message(FATAL_ERROR "The build directory must be named 'build'")
endif()




file(GLOB conf_files ${CMAKE_SOURCE_DIR}/src/configure/*)
foreach(conf_file ${conf_files})
    file(RELATIVE_PATH conf_file_rel ${CMAKE_SOURCE_DIR}/configure ${conf_file})
    configure_file(${conf_file} ${CMAKE_BINARY_DIR}/configure/${conf_file_rel})
endforeach()
list(APPEND PROJECT_INCLUDE_DIRS ${CMAKE_BINARY_DIR}/configure)




