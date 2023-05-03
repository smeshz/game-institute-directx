cmake_minimum_required(VERSION 3.25)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_EXPORT_COMPILE_COMMANDS TRUE)

# Project name
project(DirectXCmake)

# Cmake module path
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake" )

# Dependencies
find_package(DirectX REQUIRED)

set(SOURCE_FILES 
	Source/Main.cpp
	Source/CGameApp.cpp
	Source/CTimer.cpp
	Source/CObject.cpp
)

# Platform flags
list(APPEND PLATFORM_FLAGS)
if(WIN32)
	list(APPEND PLATFORM_FLAGS WIN32)
endif ()


add_executable(GameInstitute ${PLATFORM_FLAGS} ${SOURCE_FILES})

target_include_directories(GameInstitute PUBLIC Source Includes ${DirectX_INCLUDE_DIR})
target_link_libraries(GameInstitute ${DirectX_LIBRARY} ${DirectX_D3DX9_LIBRARY} Winmm)

if(CMAKE_EXPORT_COMPILE_COMMANDS)
    add_custom_command(TARGET GameInstitute POST_BUILD
            COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_BINARY_DIR}/compile_commands.json ${CMAKE_SOURCE_DIR}/compile_commands.json)
endif()