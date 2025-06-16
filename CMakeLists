cmake_minimum_required(VERSION 3.15)

# Project name and languages
project(GTA5ModMenu LANGUAGES CXX)

# --- Compiler settings ---
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# --- Build type ---
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release CACHE STRING "Build type (Debug, Release)" FORCE)
endif()

message(STATUS "Build type: ${CMAKE_BUILD_TYPE}")

# --- Output directories ---
set(BIN_DIR "${CMAKE_BINARY_DIR}/bin/${CMAKE_BUILD_TYPE}")
set(LIB_DIR "${CMAKE_BINARY_DIR}/lib/${CMAKE_BUILD_TYPE}")
set(OBJ_DIR "${CMAKE_BINARY_DIR}/obj/${CMAKE_BUILD_TYPE}")

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${BIN_DIR})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${LIB_DIR})
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${LIB_DIR})

# --- Include directories ---
include_directories(
  ${PROJECT_SOURCE_DIR}/include
  # Add external includes here, e.g.:
  # ${PROJECT_SOURCE_DIR}/external/imgui
)

# --- Component subdirectories ---
add_subdirectory(src/core)
add_subdirectory(src/features)
add_subdirectory(src/ui)
add_subdirectory(src/tools)
add_subdirectory(src/platform)
add_subdirectory(src/network)
add_subdirectory(src/audio)

# --- Main target ---
set(BUILD_AS_DLL ON CACHE BOOL "Build the mod menu as a DLL")

if(BUILD_AS_DLL)
  add_library(GTA5ModMenu SHARED
    $<TARGET_OBJECTS:core>
    $<TARGET_OBJECTS:features>
    $<TARGET_OBJECTS:ui>
    $<TARGET_OBJECTS:tools>
    $<TARGET_OBJECTS:platform>
    $<TARGET_OBJECTS:network>
    $<TARGET_OBJECTS:audio>
  )

  # Set DLL output name and prefix/suffix if needed
  set_target_properties(GTA5ModMenu PROPERTIES
    PREFIX ""     # Remove 'lib' prefix if any
    OUTPUT_NAME "GTA5ModMenu"
    RUNTIME_OUTPUT_DIRECTORY ${BIN_DIR}
  )

  # Define DLL export macro if needed
  target_compile_definitions(GTA5ModMenu PRIVATE "GTA5MODMENU_DLL_EXPORTS")

else()
  add_executable(GTA5ModMenu
    $<TARGET_OBJECTS:core>
    $<TARGET_OBJECTS:features>
    $<TARGET_OBJECTS:ui>
    $<TARGET_OBJECTS:tools>
    $<TARGET_OBJECTS:platform>
    $<TARGET_OBJECTS:network>
    $<TARGET_OBJECTS:audio>
  )
  set_target_properties(GTA5ModMenu PROPERTIES
    OUTPUT_NAME "GTA5ModMenu"
    RUNTIME_OUTPUT_DIRECTORY ${BIN_DIR}
  )
endif()

# --- Compiler options ---

# Windows-specific flags
if(MSVC)
  # Warning level 4 and exceptions enabled
  target_compile_options(GTA5ModMenu PRIVATE /W4 /EHsc /Zi /FS)

  # Debug info
  if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    target_compile_definitions(GTA5ModMenu PRIVATE "_DEBUG")
  else()
    target_compile_definitions(GTA5ModMenu PRIVATE "NDEBUG")
  endif()

else()
  # For GCC/Clang
  target_compile_options(GTA5ModMenu PRIVATE -Wall -Wextra -Wpedantic -Wshadow)

  if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    target_compile_definitions(GTA5ModMenu PRIVATE "_DEBUG")
    target_compile_options(GTA5ModMenu PRIVATE -g)
  else()
    target_compile_definitions(GTA5ModMenu PRIVATE "NDEBUG")
    target_compile_options(GTA5ModMenu PRIVATE -O2)
  endif()
endif()

# --- Linker settings ---

# Link Windows system libs
target_link_libraries(GTA5ModMenu
  user32
  gdi32
  winmm
  dxguid
  core
  features
  ui
  tools
  platform
  network
  audio
)

# --- External dependencies (placeholders) ---
# You can add third-party libs here, e.g. ImGui, DirectX SDK, or others
# Example:
# add_subdirectory(external/imgui)
# target_link_libraries(GTA5ModMenu imgui)

# --- Post-build commands (optional) ---

# Example: Copy DLL to output directory after build
# add_custom_command(TARGET GTA5ModMenu POST_BUILD
#   COMMAND ${CMAKE_COMMAND} -E copy_if_different
#     "${PROJECT_SOURCE_DIR}/external/some_dep.dll"
#     "${BIN_DIR}/some_dep.dll"
# )

# --- Summary ---
message(STATUS "Build output folder: ${BIN_DIR}")
