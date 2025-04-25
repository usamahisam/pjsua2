# Minimum required CMake version
cmake_minimum_required(VERSION 3.10)

# Project name
project(pjsua2)

# Set C++ Standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Define the Android ABI path
set(PJSIP_LIB_DIR ${CMAKE_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI})

# Create a shared library for PJSUA2
add_library(pjsua2 SHARED IMPORTED)
set_target_properties(pjsua2 PROPERTIES IMPORTED_LOCATION ${PJSIP_LIB_DIR}/libpjsua2.so)

# Add other PJSIP-related libraries
add_library(pjsip SHARED IMPORTED)
set_target_properties(pjsip PROPERTIES IMPORTED_LOCATION ${PJSIP_LIB_DIR}/libpjsip.so)

add_library(pjmedia SHARED IMPORTED)
set_target_properties(pjmedia PROPERTIES IMPORTED_LOCATION ${PJSIP_LIB_DIR}/libpjmedia.so)

add_library(pjmedia_codec SHARED IMPORTED)
set_target_properties(pjmedia_codec PROPERTIES IMPORTED_LOCATION ${PJSIP_LIB_DIR}/libpjmedia-codec.so)

add_library(pjmedia_videodev SHARED IMPORTED)
set_target_properties(pjmedia_videodev PROPERTIES IMPORTED_LOCATION ${PJSIP_LIB_DIR}/libpjmedia-videodev.so)

add_library(pjnath SHARED IMPORTED)
set_target_properties(pjnath PROPERTIES IMPORTED_LOCATION ${PJSIP_LIB_DIR}/libpjnath.so)

add_library(pjsdp SHARED IMPORTED)
set_target_properties(pjsdp PROPERTIES IMPORTED_LOCATION ${PJSIP_LIB_DIR}/libpjsdp.so)

add_library(pj SHARED IMPORTED)
set_target_properties(pj PROPERTIES IMPORTED_LOCATION ${PJSIP_LIB_DIR}/libpj.so)

add_library(pjlib_util SHARED IMPORTED)
set_target_properties(pjlib_util PROPERTIES IMPORTED_LOCATION ${PJSIP_LIB_DIR}/libpjlib-util.so)

# Link all PJSIP libraries to PJSUA2
target_link_libraries(pjsua2
    pjsip
    pjmedia
    pjmedia_codec
    pjmedia_videodev
    pjnath
    pjsdp
    pj
    pjlib_util
    log  # Android log library
    android  # Android native API
)
