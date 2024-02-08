cmake_minimum_required(VERSION 3.10)

project(ScriptHookV)

# Set the C++ standard
set(CMAKE_CXX_STANDARD 14)

# Add source files
set(SOURCES
    src/dllmain.cpp
    src/stdafx.cpp
)

# Add header files
set(HEADERS
    src/stdafx.h
)

# Define the shared library target
add_library(ScriptHookV SHARED ${SOURCES} ${HEADERS})

# Set compiler flags and options
target_compile_options(ScriptHookV PRIVATE
    $<$<CONFIG:Debug>:/DDEBUG /MDd /Zi>
    $<$<CONFIG:Release>:/DNDEBUG /MD /O2>
)

# Define preprocessor definitions
target_compile_definitions(ScriptHookV PRIVATE
    $<$<BOOL:${WIN32}>:_WINDOWS>
    $<$<BOOL:${CMAKE_SIZEOF_VOID_P} EQUAL 8>:_WIN64>
)

# Additional configurations based on platform or build configuration
