cmake_minimum_required(VERSION 3.15)

project(HushMe)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# ---- Torch ----
set(CMAKE_PREFIX_PATH "/home/peter/libtorch")
find_package(Torch REQUIRED)

# ---- SndFile ----
find_package(PkgConfig REQUIRED)
pkg_check_modules(SNDFILE REQUIRED sndfile)

# ---- Executable ----
add_executable(HushMe
    src/main.cpp
    src/vad.cpp
    src/dsp_utils.cpp
    src/ml_processor.cpp
    src/hybrid_processor.cpp
)

# ---- Include & link ----
target_include_directories(HushMe PRIVATE ${SNDFILE_INCLUDE_DIRS})
target_link_directories(HushMe PRIVATE ${SNDFILE_LIBRARY_DIRS})

target_link_libraries(HushMe PRIVATE
    "${TORCH_LIBRARIES}"
    ${SNDFILE_LIBRARIES}
)

# ---- macOS RPATH fix ----
if(APPLE)
    set(CMAKE_INSTALL_RPATH "${TORCH_INSTALL_PREFIX}/lib")
endif()

