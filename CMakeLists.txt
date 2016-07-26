cmake_minimum_required(VERSION 3.2)

project(tinyxmlSTL VERSION 2.8.2 LANGUAGES CXX)

if(MSVC)
    set(CMAKE_DEBUG_POSTFIX "d")
endif()

add_library(tinyxmlSTL STATIC
  tinyxml.h
  tinyxml.cpp
  tinyxmlerror.cpp
  tinyxmlparser.cpp
)

target_compile_definitions(tinyxmlSTL
  PRIVATE TIXML_USE_STL
  _CRT_SECURE_NO_DEPRECATE
  _CRT_NONSTDC_NO_DEPRECATE
)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
  ${CMAKE_CURRENT_BINARY_DIR}/tinyxmlSTL-config-version.cmake
  VERSION ${PROJECT_VERSION}
  COMPATIBILITY AnyNewerVersion
)
install(TARGETS tinyxmlSTL EXPORT tinyxmlSTL
  RUNTIME DESTINATION bin
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib)
install(FILES
  tinystr.h
  tinyxml.h
  DESTINATION include)

install(EXPORT tinyxmlSTL
  FILE
    tinyxmlSTL.cmake
  NAMESPACE
    tinyxml::
  DESTINATION
    lib/cmake/tinyxmlSTL
)
install(
  FILES
    cmake/tinyxmlSTL-config.cmake
    ${CMAKE_CURRENT_BINARY_DIR}/tinyxmlSTL-config-version.cmake
  DESTINATION
    lib/cmake/tinyxmlSTL
)

export(TARGETS tinyxmlSTL
    FILE tinyxmlSTL-config.cmake
    NAMESPACE tinyxml::
)
