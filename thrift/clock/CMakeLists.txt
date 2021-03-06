# Copyright (C) 2007-2015 Istituto Italiano di Tecnologia ADVR & iCub Facility & RBCS Department
# Authors: Enrico Mingo, Alessio Rocchi, Mirko Ferrati, Silvio Traversaro, Alessandro Settimi and Francesco Romano
# CopyPolicy: Released under the terms of the LGPLv2.1 or later, see LGPL.TXT

cmake_minimum_required(VERSION 2.8.11)

PROJECT(RPC_clock)

yarp_idl_to_dir(clock_rpc.thrift ${CMAKE_CURRENT_SOURCE_DIR}/autogenerated CLOCKRPC_SRC CLOCKRPC_HEADERS CLOCKRPC_INCLUDES)

include_directories(${CLOCKRPC_INCLUDES} ${YARP_INCLUDE_DIRS})
add_library(gazebo_yarp_rpc_clock SHARED ${CLOCKRPC_SRC} ${CLOCKRPC_HEADERS})
target_link_libraries(gazebo_yarp_rpc_clock ${YARP_LIBRARIES})


target_include_directories(gazebo_yarp_rpc_clock PUBLIC 
                            "$<BUILD_INTERFACE:${CLOCKRPC_INCLUDES}>"
                            "$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/gazebo>")

set_property(TARGET gazebo_yarp_rpc_clock PROPERTY PUBLIC_HEADER ${CLOCKRPC_HEADERS})

install(TARGETS gazebo_yarp_rpc_clock
                LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
                PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/gazebo)

