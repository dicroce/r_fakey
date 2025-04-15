cmake_minimum_required(VERSION 3.14)
set(PROJECT_VERSION_MAJOR 0)
set(PROJECT_VERSION_MINOR 0)
set(PROJECT_VERSION_PATCH 1)
project(r_fakey VERSION ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}.${PROJECT_VERSION_PATCH})

include(r_build.txt)
include(GSTREAMERConfig.cmake REQUIRED)
include(FFMPEGConfig.cmake REQUIRED)
include(FetchContent)

FetchContent_Declare(
    r_utils
    GIT_REPOSITORY https://github.com/dicroce/r_utils.git
    GIT_TAG        main
    FIND_PACKAGE_ARGS NAMES r_utils
)
FetchContent_MakeAvailable(r_utils)

FetchContent_Declare(
    r_av
    GIT_REPOSITORY https://github.com/dicroce/r_av.git
    GIT_TAG        main
    FIND_PACKAGE_ARGS NAMES r_av
)
FetchContent_MakeAvailable(r_av)

add_library(
    r_fakey
    include/r_fakey/r_fake_camera.h
    source/r_fake_camera.cpp
)

target_include_directories(
    r_fakey PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

target_link_libraries(
    r_fakey
    r_av
    ${GST_LIBS}
    ${FFMPEG_LIBS}
)

configure_dev_package("r_fakey" "A C++ library that useful for making fake cameras.")
