cmake_minimum_required(VERSION 3.16)
set(PROJECT_NAME example_project)
project(${PROJECT_NAME} VERSION 1.0.0)

include(FetchContent)

# configure_file(
#   ${CMAKE_SOURCE_DIR}/include/config.h.in
#   ${CMAKE_SOURCE_DIR}/include/config.h
# )

enable_language(C CXX)
set(CMAKE_C_STANDARD 99)
set(CMAKE_CXX_STANDARD 17)
# set(CMAKE_CUDA_ARCHITECTURES 87 89)
# enable_language(CUDA) 


# 옵션: 실행파일도 빌드할지 여부
option(BUILD_EXE "Build executable for testing" ON)

# POSIX 정의
if (UNIX)
    add_definitions(-D_GNU_SOURCE)
endif()

# include 폴더
include_directories(${CMAKE_SOURCE_DIR}/include)

# 소스 파일 목록
set(SRC_FILES
    src/main.cpp
)


# find_package(CUDAToolkit REQUIRED)
add_subdirectory(external/spdlog)
add_subdirectory(external/CLI11)


# ▶ 실행파일은 선택적으로 빌드
if (BUILD_EXE)
    add_executable(${PROJECT_NAME} ${SRC_FILES})
    target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_SOURCE_DIR}/include)

    if (UNIX)
        target_compile_definitions(${PROJECT_NAME} PRIVATE _LINUX)
        target_link_libraries(${PROJECT_NAME} PRIVATE pthread m)
    elseif (WIN32)
        target_compile_definitions(${PROJECT_NAME} PRIVATE _WIN32 _CONSOLE)
    endif()
endif()

find_package(Threads REQUIRED)

target_link_libraries(${PROJECT_NAME} PRIVATE spdlog::spdlog)
target_link_libraries(${PROJECT_NAME} PRIVATE CLI11::CLI11)

target_link_libraries(${PROJECT_NAME} PRIVATE Threads::Threads)
# target_link_libraries(${PROJECT_NAME} PRIVATE CUDA::cudart)