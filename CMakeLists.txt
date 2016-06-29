cmake_minimum_required(VERSION 3.2)

project(tinyxml VERSION 2.8.2 LANGUAGES CXX)

if(MSVC)
    set(CMAKE_DEBUG_POSTFIX "d")
    add_definitions(-D_CRT_SECURE_NO_DEPRECATE)
    add_definitions(-D_CRT_NONSTDC_NO_DEPRECATE)
endif()

add_library(tinyxml
  tinystr.h
  tinyxml.h
  tinystr.cpp
  tinyxml.cpp
  )

install(TARGETS tinyxml
  RUNTIME DESTINATION bin
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib)
install(FILES
  tinystr.h
  tinyxml.h
  DESTINATION include)