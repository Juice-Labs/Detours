cmake_minimum_required(VERSION 3.5)

project(detours)

set(BITS 64)
set(MACHINE X64)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/CMakeLists.txt.in ${CMAKE_CURRENT_BINARY_DIR}/CMakeLists.64.txt @ONLY)
include(${CMAKE_CURRENT_BINARY_DIR}/CMakeLists.64.txt)

set(BITS 32)
set(MACHINE X86)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/CMakeLists.txt.in ${CMAKE_CURRENT_BINARY_DIR}/CMakeLists.32.txt @ONLY)
include(${CMAKE_CURRENT_BINARY_DIR}/CMakeLists.32.txt)
