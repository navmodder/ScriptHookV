cmake_minimum_required(VERSION 3.10)

# Project name
project(ScriptHookV)

# Source files
set(SOURCES
    src/Config/Config.cpp
    src/Core/Core.cpp
    src/Main.cpp
    src/Pch/Common.cpp
)

# Header files
set(HEADERS
    src/Config/Config.hpp
    src/Core/Core.hpp
    src/Exports/Exports.hpp
    src/Json/Json.hpp
    src/Pch/Common.hpp
)

# Add library
add_library(${PROJECT_NAME} SHARED ${SOURCES} ${HEADERS})

# Include directories
target_include_directories(${PROJECT_NAME} PRIVATE src)

# Set compile options
target_compile_options(${PROJECT_NAME} PRIVATE
    $<$<CONFIG:Debug>: /W3 /DWIN32 /D_DEBUG /DSCRIPTHOOKV_EXPORTS /D_WINDOWS /D_USRDLL /GR /EHsc>
    $<$<CONFIG:Release>: /W3 /DNDEBUG /DWIN32 /DSCRIPTHOOKV_EXPORTS /D_WINDOWS /D_USRDLL /GR /EHsc>
)

# Set precompiled header
target_precompile_headers(${PROJECT_NAME} PRIVATE "src/Pch/Common.hpp")

# Set Windows specific options
if(WIN32)
    target_compile_definitions(${PROJECT_NAME} PRIVATE UNICODE _UNICODE)
    set_target_properties(${PROJECT_NAME} PROPERTIES WINDOWS_EXPORT_ALL_SYMBOLS ON)
endif()
