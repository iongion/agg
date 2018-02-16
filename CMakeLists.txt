cmake_minimum_required(VERSION 2.8.12)
project(agg)
set (agg_VERSION_MAJOR 2)
set (agg_VERSION_MINOR 5)

add_definitions("-std=c++11")

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

# this is the "object library" target: compiles the sources only once
add_library(objlib OBJECT ${libsrc})

# shared libraries need PIC
set_property(TARGET ${objlib} PROPERTY POSITION_INDEPENDENT_CODE 1)

# shared and static libraries built from the same object files
# add_library(agg SHARED $<TARGET_OBJECTS:objlib>)
add_library(agg STATIC $<TARGET_OBJECTS:objlib>)

# target_link_libraries(agg ${CONAN_LIBS})
