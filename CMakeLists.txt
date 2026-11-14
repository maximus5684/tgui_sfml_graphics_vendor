cmake_minimum_required(VERSION 3.10)
project(tgui_sfml_graphics_vendor)

find_package(ament_cmake_auto REQUIRED)
ament_auto_find_build_dependencies()

# SFML 3 uses capitalized component names; SFML 2 uses lowercase.
find_package(SFML 3 CONFIG QUIET COMPONENTS Graphics)
if(NOT SFML_FOUND)
  find_package(SFML 2.5 CONFIG REQUIRED COMPONENTS graphics)
endif()

ament_vendor(${PROJECT_NAME}
  SATISFIED FALSE
  VCS_URL https://github.com/texus/TGUI.git
  VCS_VERSION v1.10.0
  CMAKE_ARGS
    -DCMAKE_BUILD_TYPE=Release
    -DTGUI_BACKEND=SFML_GRAPHICS
    -DTGUI_SHARED_LIBS=ON
    -DTGUI_CXX_STANDARD=17
    -DTGUI_BUILD_GUI_BUILDER=OFF
  GLOBAL_HOOK
)

ament_auto_package()
