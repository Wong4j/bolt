cmake_minimum_required(VERSION 3.2)

file(GLOB BOLT_CONFIGURE_FILE $ENV{BOLT_ROOT}/bolt.cmake ${BOLT_ROOT}/bolt.cmake)
if (BOLT_CONFIGURE_FILE)
    include(${BOLT_CONFIGURE_FILE})
else (BOLT_CONFIGURE_FILE)
    message(FATAL_ERROR "
FATAL: can not find bolt.cmake in <BOLT_ROOT> directory,
       please set shell or cmake environment variable BOLT_ROOT.
    ")
endif (BOLT_CONFIGURE_FILE)

project(gclBinary)

set_policy()

SET(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${BOLT_ROOT}/cmakes")
find_package(Gcl)
find_package(Uni)

set_c_cxx_flags()

set_test_c_cxx_flags()

add_executable(gcl_binary clbinary.cpp)
TARGET_LINK_LIBRARIES(gcl_binary ${OPENCL_LIBRARIES} -Wl,-allow-shlib-undefined, -static-libstdc++)
