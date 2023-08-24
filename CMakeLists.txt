cmake_minimum_required(VERSION 3.10)

project(HysBase LANGUAGES CXX C)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILECOMMANDS ON)

find_program(CCACHE_PROGRAM ccache) # Compilation speed up: https://ccache.dev

if(CCACHE_PROGRAM)
    message(STATUS "Found CCache: ${CCACHE_PROGRAM}")
    set_property(GLOBAL PROPERTY RULE_LAUNCH_COMPILE ${CCACHE_PROGRAM})
    set_property(GLOBAL PROPERTY RULE_LAUNCH_LINK ${CCACHE_PROGRAM})
endif()

file(GLOB_RECURSE sources CONFIGURE_DEPENDS src/*.cpp)
file(GLOB_RECURSE headers CONFIGURE_DEPENDS include/*.h include/*.hpp)

add_executable(${PROJECT_NAME} ${sources} ${headers})
target_include_directories(${PROJECT_NAME} PUBLIC include)

# fmt
add_subdirectory(thirdparty/fmt)
target_link_libraries(HysBase PRIVATE fmt::fmt)

target_compile_definitions(${PROJECT_NAME} PUBLIC -DOPENGLTUTOR_HOME=\"${CMAKE_CURRENT_SOURCE_DIR}/\")