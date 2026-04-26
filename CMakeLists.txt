cmake_minimum_required(VERSION 3.10)
# ImGUI use tag v1.92.7-docking
project(imgui_lib VERSION 1.92.7)

include(GNUInstallDirs)

find_package(OpenGL REQUIRED)
find_package(SDL2 REQUIRED)

set(IMGUI_SRCS
    imgui.cpp 
    imgui_draw.cpp 
    imgui_widgets.cpp 
    imgui_tables.cpp 
    imgui_demo.cpp
    backends/imgui_impl_sdl2.cpp
    backends/imgui_impl_opengl3.cpp
)

add_library(imgui SHARED ${IMGUI_SRCS})

target_link_libraries(imgui PUBLIC 
    SDL2::SDL2
    OpenGL::GL
)

target_include_directories(imgui PUBLIC 
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/backends>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/imgui>
)

install(TARGETS imgui 
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} 
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

install(FILES 
    imgui.h
    imconfig.h 
    imgui_internal.h
    imstb_rectpack.h 
    imstb_textedit.h
    imstb_truetype.h 
    backends/imgui_impl_sdl2.h
    backends/imgui_impl_opengl3.h
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/imgui
)