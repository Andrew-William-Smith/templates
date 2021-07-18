# Copyright (c) ${YEAR}, Andrew Smith <aws@awsmith.us>
# SPDX-License-Identifier: MIT

cmake_minimum_required(VERSION 3.16)
project(${PROJECT_NAME} C)
set(CMAKE_C_STANDARD 17)

# Set the host compiler to be fairly strict by default.
if(CMAKE_C_COMPILER_ID MATCHES "Clang" OR CMAKE_C_COMPILER_ID MATCHES "GNU")
    add_compile_options(-Wall -Wextra -Werror)
elseif(CMAKE_C_COMPILER_ID MATCHES "MSVC")
    add_compile_options(/W3 /WX)
else()
    message(WARNING "Compiler with ID ${CMAKE_C_COMPILER_ID} is not recognised.")
endif()

# Enable debugging macros in debug builds.
if(CMAKE_BUILD_TYPE MATCHES "Debug")
    message(STATUS "This is a debug build: debugging checks will be enabled.")
    add_compile_definitions(${PROJECT_UPPER}_DEBUG_ENABLED)
endif()

# Configure common directories used throughout the project.
set(CMAKE_INSTALL_PREFIX ${PROJECT_SOURCE_DIR})
set(${PROJECT_UPPER}_INSTALL_BIN_DIR ${CMAKE_INSTALL_PREFIX}/bin)
set(${PROJECT_UPPER}_INSTALL_INCLUDE_DIR ${CMAKE_INSTALL_PREFIX}/include)
set(${PROJECT_UPPER}_INSTALL_LIB_DIR ${CMAKE_INSTALL_PREFIX}/lib)

include_directories(${${PROJECT_UPPER}_INSTALL_INCLUDE_DIR})
add_subdirectory(src)
