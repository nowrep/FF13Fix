cmake_minimum_required(VERSION 3.10)

project(ff13fix VERSION 1.0.0)

set(CMAKE_CXX_FLAGS "-fpermissive")

add_definitions(
    -DSPDLOG_DISABLE_DEFAULT_LOGGER
    -DSPDLOG_WCHAR_TO_UTF8_SUPPORT
    -DWIN32
    -DNDEBUG
    -D_WINDOWS
    -D_USRDLL
    )

set(ff13fix_srcs
    d3d9ex/AutoFix.cpp
    d3d9ex/AutoFix.h
    d3d9ex/Context.cpp
    d3d9ex/Context.h
    d3d9ex/dllmain.cpp
    d3d9ex/exports.def
    d3d9ex/IDirect3D9.cpp
    d3d9ex/IDirect3D9.h
    d3d9ex/IDirect3DDevice9.cpp
    d3d9ex/IDirect3DDevice9.h
    d3d9ex/Settings.h
    d3d9ex/stdafx.cpp
    d3d9ex/stdafx.h
    d3d9ex/targetver.h
    d3d9ex/VertexFix.cpp
    d3d9ex/Wrapper.h
    d3d9ex/XInputManager.cpp
    d3d9ex/XInputManager.h
)

add_subdirectory(Deps/MinHook)
add_subdirectory(Deps/spdlog)

include_directories(Common)

add_library(ff13fix SHARED ${ff13fix_srcs})
target_link_libraries(ff13fix spdlog minhook d3d9 xinput9_1_0 -static)
