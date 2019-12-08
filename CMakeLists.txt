cmake_minimum_required(VERSION 3.4.1)
project(yoga VERSION 1.0.0 DESCRIPTION "yoga description")
include(GNUInstallDirs)

set(CMAKE_VERBOSE_MAKEFILE on)

add_compile_options(
    -fno-omit-frame-pointer
    -fexceptions
    -fvisibility=hidden
    -ffunction-sections
    -fdata-sections
    -Wall
    -std=c++11)

add_library(yoga SHARED
    yoga/YGEnums.cpp
    yoga/Utils.cpp
    yoga/YGNode.cpp
    yoga/YGStyle.cpp
    yoga/Yoga.cpp
    yoga/YGConfig.cpp
    yoga/YGLayout.cpp
    yoga/YGNodePrint.cpp
    yoga/YGValue.cpp
    yoga/log.cpp)

target_include_directories(yoga PRIVATE .)

configure_file(yoga.pc.in yoga.pc @ONLY)
set_target_properties(yoga PROPERTIES CXX_STANDARD 11)
set_target_properties(yoga PROPERTIES VERSION ${PROJECT_VERSION})
set_target_properties(yoga PROPERTIES PUBLIC_HEADER "yoga/Bitfield.h;yoga/CompactValue.h;yoga/Utils.h;yoga/YGConfig.h;yoga/YGEnums.h;yoga/YGFloatOptional.h;yoga/YGLayout.h;yoga/YGMacros.h;yoga/YGNode.h;yoga/YGNodePrint.h;yoga/YGStyle.h;yoga/YGValue.h;yoga/Yoga-internal.h;yoga/Yoga.h;yoga/log.h")

install(TARGETS yoga
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/yoga)
