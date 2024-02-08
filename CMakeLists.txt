cmake_minimum_required(VERSION 3.10)

project(ScriptHookV)

# Set the C++ standard
set(CMAKE_CXX_STANDARD 14)

# Add source files
set(SOURCES
    src/stdafx.h
    src/dllmain.cpp
    src/stdafx.cpp
)

# Define the executable or library
add_library(ScriptHookV SHARED ${SOURCES})

# Set compiler flags and options
target_compile_options(ScriptHookV PRIVATE
    $<$<CONFIG:Debug>:/DDEBUG /MDd /Zi>
    $<$<CONFIG:Release>:/DNDEBUG /MD /O2>
)

# Additional configurations based on platform
if(WIN32)
    if(CMAKE_SIZEOF_VOID_P EQUAL 8)
        set_target_properties(ScriptHookV PROPERTIES COMPILE_DEFINITIONS _WIN64)
    endif()
endif()
