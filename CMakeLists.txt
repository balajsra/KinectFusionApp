cmake_minimum_required(VERSION 3.0)

project(KinectFusionApplication)

# Setting some paths
set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/build)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

# Path of find modules
set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake ${CMAKE_MODULE_PATH})

# Targets
add_subdirectory(KinectFusionLib)
add_subdirectory(KinectFusionApp)

# Set CUDA architecture version
SET(CUDA_NVCC_FLAGS ${CUDA_NVCC_FLAGS};-O3 -gencode arch=compute_61,code=sm_61)
