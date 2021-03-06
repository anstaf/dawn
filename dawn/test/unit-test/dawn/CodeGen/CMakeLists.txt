##===------------------------------------------------------------------------------*- CMake -*-===##
##                          _
##                         | |
##                       __| | __ ___      ___ ___
##                      / _` |/ _` \ \ /\ / / '_  |
##                     | (_| | (_| |\ V  V /| | | |
##                      \__,_|\__,_| \_/\_/ |_| |_| - Compiler Toolchain
##
##
##  This file is distributed under the MIT License (MIT).
##  See LICENSE.txt for details.
##
##===------------------------------------------------------------------------------------------===##
include(GoogleTest)

file(COPY input DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
file(COPY reference DESTINATION ${CMAKE_CURRENT_BINARY_DIR})

foreach(backend IN ITEMS Cuda Naive)
  set(executable ${PROJECT_NAME}UnittestCodeGen${backend})
  add_executable(${executable} ${backend}/Test${backend}CodeGen.cpp Stencils.cpp)
  target_add_dawn_standard_props(${executable})
  target_include_directories(${executable} PRIVATE $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>)
  target_link_libraries(${executable} DawnUnittest gtest gtest_main)
  gtest_discover_tests(${executable} TEST_PREFIX "Dawn::Unit::CodeGen::"
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    DISCOVERY_TIMEOUT 30
  )
endforeach()

foreach(backend IN ITEMS Cuda-Ico Naive-Ico)
  set(executable ${PROJECT_NAME}UnittestCodeGen${backend})
  add_executable(${executable} ${backend}/Test${backend}CodeGen.cpp UnstructuredStencils.cpp)
  target_add_dawn_standard_props(${executable})
  target_include_directories(${executable} PRIVATE $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>)
  target_link_libraries(${executable} DawnUnittest gtest gtest_main)
  gtest_discover_tests(${executable} TEST_PREFIX "Dawn::Unit::UnstructuredCodeGen::"
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    DISCOVERY_TIMEOUT 30
  )
endforeach()