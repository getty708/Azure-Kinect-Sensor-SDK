# Copyright (c) Microsoft Corporation. All rights reserved.
# Licensed under the MIT License.
cmake_minimum_required(VERSION 3.10.2)
set(libjpeg-turbo_DIR /opt/libjpeg-turbo/lib64/cmake/libjpeg-turbo)
include_directories(/opt/libjpeg-turbo/include/)
# link_directories(/opt/libjpeg-turbo/lib64/)

find_package(k4a)
find_package(k4arecord)
find_package(libjpeg-turbo)

if (OpenCV_REQUIRED)
    find_package(OpenCV REQUIRED)
else()
    find_package(OpenCV)
endif ()

add_executable(transformation_example 
    main.cpp
    transformation_helpers.cpp
    transformation_helpers.h)

target_link_libraries(transformation_example PRIVATE
    k4a::k4a
    k4a::k4arecord
    # libjpeg-turbo::libjpeg-turbo
    # libjpeg-turbo::libturbojpeg
    # libturbojpeg
    /opt/libjpeg-turbo/lib64/libturbojpeg.so
    )
