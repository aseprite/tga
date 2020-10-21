# Aseprite TGA Library
# Copyright (C) 2020  Igara Studio S.A.
project(tgalib)

add_library(tga-lib
  decoder.cpp
  encoder.cpp
  image_iterator.cpp
  stdio.cpp)

set_target_properties(tga-lib PROPERTIES PUBLIC_HEADER "tga.h")
install(TARGETS tga-lib ARCHIVE DESTINATION lib PUBLIC_HEADER DESTINATION include)


