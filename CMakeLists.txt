cmake_minimum_required(VERSION 3.20)
project(Foo CXX)

set(SOURCES
        ${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp
)

add_executable(foo ${SOURCES})
target_include_directories(foo PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
find_package(fmt  REQUIRED)

target_compile_options(foo PRIVATE
    $<$<CONFIG:Debug>:
        -fsanitize=address,leak,undefined 
        -pedantic 
        -Wall 
        -Wextra 
        -Wconversion 
        -Wundef 
        -Werror  
        -Wno-unused-parameter
        -Wno-unused-variable
    >
)

target_link_options(foo PRIVATE
    $<$<CONFIG:Debug>:
        -fsanitize=address,leak,undefined
    >
)

target_compile_features(foo
    PRIVATE
        cxx_std_20
)

target_link_libraries(foo PRIVATE
    fmt::fmt
)

if (BUILD_TESTING)
    include(CTest)
    enable_testing()
    add_subdirectory(LibTests)
endif()
