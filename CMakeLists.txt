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
)
FetchContent_MakeAvailable(r_utils)

FetchContent_Declare(
    r_av
    GIT_REPOSITORY https://github.com/dicroce/r_av.git
    GIT_TAG        main
)
FetchContent_MakeAvailable(r_av)

add_library(
    r_fakey
    include/r_fakey/r_fake_camera.h
    source/r_fake_camera.cpp
)

target_include_directories(
    r_fakey PUBLIC
    include
    ${r_utils_SOURCE_DIR}/include
    ${r_av_SOURCE_DIR}/include
    ${GST_INCLUDE_DIRS}
    ${FFMPEG_INCLUDE_DIRS}
)

target_link_directories(
    r_fakey PUBLIC
    ${GST_LIB_DIRS}
    ${FFMPEG_LIB_DIRS}
)

target_link_libraries(
    r_fakey
    ${GST_LIBS}
    ${FFMPEG_LIBS}
)
