cmake_minimum_required(VERSION 3.10)

project(HysBase LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 23)

# fmt
add_subdirectory(thirdparty/fmt)

add_executable(HysBase main.cpp)

target_link_libraries(HysBase PRIVATE
    fmt::fmt
)