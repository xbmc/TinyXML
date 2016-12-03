cmake_minimum_required(VERSION 3.2)

project(tinyXML VERSION 2.8.2 LANGUAGES CXX)

if(MSVC)
    set(CMAKE_DEBUG_POSTFIX "d")
endif()

add_library(tinyXML STATIC
  tinyxml.h
  tinyxml.cpp
  tinyxmlerror.cpp
  tinyxmlparser.cpp
)

target_compile_definitions(tinyXML
  PRIVATE
  TIXML_USE_STL
  _CRT_SECURE_NO_DEPRECATE
  _CRT_NONSTDC_NO_DEPRECATE
  INTERFACE
  TIXML_USE_STL
)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
  ${CMAKE_CURRENT_BINARY_DIR}/tinyXML-config-version.cmake
  VERSION ${PROJECT_VERSION}
  COMPATIBILITY AnyNewerVersion
)
install(TARGETS tinyXML EXPORT tinyXML
  RUNTIME DESTINATION bin
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib)
install(FILES
  tinystr.h
  tinyxml.h
  DESTINATION include)

install(EXPORT tinyXML
  FILE
    tinyXML.cmake
  NAMESPACE
    tinyxml::
  DESTINATION
    lib/cmake/tinyXML
)
install(
  FILES
    cmake/tinyXML-config.cmake
    ${CMAKE_CURRENT_BINARY_DIR}/tinyXML-config-version.cmake
  DESTINATION
    lib/cmake/tinyXML
)

export(TARGETS tinyXML
    FILE tinyXML-config.cmake
    NAMESPACE tinyxml::
)
