# SPDX-License-Identifier: BSD-3-Clause
# Copyright Contributors to the OpenColorIO Project.

configure_file("OpenColorABI.h.in" "${CMAKE_CURRENT_BINARY_DIR}/OpenColorABI.h" @ONLY)
add_library(public_api INTERFACE)

set_property(TARGET public_api 
	PROPERTY INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_CURRENT_SOURCE_DIR}/..;${CMAKE_CURRENT_SOURCE_DIR};${CMAKE_CURRENT_BINARY_DIR};${CMAKE_CURRENT_BINARY_DIR}/OpenColorIO
)

add_dependencies(public_api "${CMAKE_CURRENT_BINARY_DIR}/OpenColorABI.h")

# public interface

file(GLOB_RECURSE core_export_headers "${CMAKE_CURRENT_SOURCE_DIR}/*.h")
list(APPEND core_export_headers ${CMAKE_CURRENT_BINARY_DIR}/OpenColorABI.h)

install(FILES ${core_export_headers}
    DESTINATION include/OpenColorIO)
