cmake_minimum_required(VERSION 3.20)
project(pthash)

add_subdirectory(external/xxHash/cmake_unofficial)

add_library(pthash INTERFACE)
target_link_libraries(pthash INTERFACE xxhash)
target_include_directories(pthash INTERFACE scoped-include)
set_target_properties(pthash PROPERTIES CXX_STANDARD 17)

if (NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release")
endif ()

if (PTHASH_ENABLE_ALL_ENCODERS)
  MESSAGE(STATUS "compiling pthash with all encoders")
  target_compile_definitions(pthash INTERFACE PTHASH_ENABLE_ALL_ENCODERS)
endif()
