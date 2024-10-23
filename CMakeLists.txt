cmake_minimum_required(VERSION 3.10)  
project(google_iconvg)

add_library(google_iconvg STATIC 
    src/c/broken.c
    src/c/cairo.c
    src/c/color.c
    src/c/debug.c
    src/c/decoder.c
    src/c/error.c
    src/c/matrix.c
    src/c/paint.c
    src/c/rectangle.c
    src/c/skia.c
    example/iconvg-to-png/iconvg-to-png.c
)

include_directories(
    /opt/homebrew/Cellar/libpng/1.6.44/include
)

target_link_libraries(google_iconvg PRIVATE
    /opt/homebrew/Cellar/libpng/1.6.44/lib/libpng.a
)

find_program(AFL_C_COMPILER afl-clang-fast)
find_program(AFL_CXX_COMPILER afl-clang-fast++)
set(CMAKE_C_COMPILER ${AFL_C_COMPILER})
set(CMAKE_CXX_COMPILER ${AFL_CXX_COMPILER})

target_include_directories(google_iconvg PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})