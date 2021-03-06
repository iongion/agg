cmake_minimum_required(VERSION 3.5.1)
project(agg)

find_package(X11 REQUIRED)

include_directories(${X11_INCLUDE_DIR})
link_directories(${X11_LIBRARIES})

set (agg_VERSION_MAJOR 2)
set (agg_VERSION_MINOR 5)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

# list of header files
include_directories(include)

# list of source files
set(
  libsrc
  src/agg_arc.cpp
  src/agg_arrowhead.cpp
  src/agg_bezier_arc.cpp
  src/agg_bspline.cpp
  src/agg_curves.cpp
  src/agg_embedded_raster_fonts.cpp
  src/agg_gsv_text.cpp
  src/agg_image_filters.cpp
  src/agg_line_aa_basics.cpp
  src/agg_line_profile_aa.cpp
  src/agg_rounded_rect.cpp
  src/agg_sqrt_tables.cpp
  src/agg_trans_affine.cpp
  src/agg_trans_double_path.cpp
  src/agg_trans_single_path.cpp
  src/agg_trans_warp_magnifier.cpp
  src/agg_vcgen_bspline.cpp
  src/agg_vcgen_contour.cpp
  src/agg_vcgen_dash.cpp
  src/agg_vcgen_markers_term.cpp
  src/agg_vcgen_smooth_poly1.cpp
  src/agg_vcgen_stroke.cpp
  src/agg_vpgen_clip_polygon.cpp
  src/agg_vpgen_clip_polyline.cpp
  src/agg_vpgen_segmentator.cpp
  # ctrl
  src/ctrl/agg_bezier_ctrl.cpp
  src/ctrl/agg_cbox_ctrl.cpp
  src/ctrl/agg_gamma_ctrl.cpp
  src/ctrl/agg_gamma_spline.cpp
  src/ctrl/agg_polygon_ctrl.cpp
  src/ctrl/agg_rbox_ctrl.cpp
  src/ctrl/agg_scale_ctrl.cpp
  src/ctrl/agg_slider_ctrl.cpp
  src/ctrl/agg_spline_ctrl.cpp
  # font
  font_freetype/agg_font_freetype.cpp
  # gpc
  gpc/gpc.c
)

# objects
add_library(core OBJECT ${libsrc})
set_property(TARGET core PROPERTY POSITION_INDEPENDENT_CODE ON)

# shared
add_library(agg SHARED $<TARGET_OBJECTS:core>)

# static
add_library(agg_static STATIC $<TARGET_OBJECTS:core>)
set_target_properties(agg_static PROPERTIES OUTPUT_NAME agg)

# examples
add_executable(aa_demo examples/aa_demo.cpp src/platform/X11/agg_platform_support.cpp ${X11_LIBRARIES})
target_link_libraries(aa_demo LINK_PUBLIC agg_static)
