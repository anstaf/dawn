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

add_test(NAME Dawn4Py::Unit::structured
  COMMAND ${CMAKE_COMMAND} -E env PYTHONPATH=${DAWN4PY_MODULE_DIR}:${PROTOBUF_PYTHON_DIR}
  ${Python3_EXECUTABLE} -m pytest -v ${CMAKE_CURRENT_SOURCE_DIR}/test_structured.py
)

add_test(NAME Dawn4Py::Unit::unstructured
  COMMAND ${CMAKE_COMMAND} -E env PYTHONPATH=${DAWN4PY_MODULE_DIR}:${PROTOBUF_PYTHON_DIR}
  ${Python3_EXECUTABLE} -m pytest -v ${CMAKE_CURRENT_SOURCE_DIR}/test_unstructured.py
)
