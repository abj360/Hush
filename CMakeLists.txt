cmake_minimum_required(VERSION 3.15)
project(Hush)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_PREFIX_PATH "/Home/peter/libtorch")

find_package(Torch REQUIRED)
find_package(SndFile REQUIRED)

add_executable(NoiseCancellation
    src/main.cpp
    src/vad.cpp
    src/dsp_utils.cpp
    src/ml_processor.cpp
    src/hybrid_processor.cpp
)

target_link_libraries(Hush  PRIVATE "${TORCH_LIBRARIES}" SndFile::sndfile)

if(APPLE)
    set(CMAKE_INSTALL_RPATH "${TORCH_INSTALL_PREFIX}/lib")
endif()
