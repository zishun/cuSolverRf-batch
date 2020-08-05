cmake_minimum_required(VERSION 3.10)

set(PROJECT_NAME cuSolverRfBatch)
project (${PROJECT_NAME} LANGUAGES C CXX CUDA)

set(SRC_FILES
    mmio_wrapper.cpp
    cuSolverRfBatch.cpp
)

add_executable(${PROJECT_NAME} ${SRC_FILES})
add_library(mmio mmio.c)

# CUDA
find_library(CUDA_LIBRARY_CUDART cudart ${CMAKE_CUDA_IMPLICIT_LINK_DIRECTORIES})
find_library(CUDA_LIBRARY_CUSOLVER cusolver ${CMAKE_CUDA_IMPLICIT_LINK_DIRECTORIES})
find_library(CUDA_LIBRARY_CUSPARSE cusparse ${CMAKE_CUDA_IMPLICIT_LINK_DIRECTORIES})
target_include_directories(
    ${PROJECT_NAME}
    PRIVATE
    ${CMAKE_CUDA_TOOLKIT_INCLUDE_DIRECTORIES}
    "./inc/"
)
target_link_libraries(
    ${PROJECT_NAME}
    ${CUDA_LIBRARY_CUDART}
    ${CUDA_LIBRARY_CUSOLVER}
    ${CUDA_LIBRARY_CUSPARSE}
    mmio
)

if (MSVC)
    add_compile_options("$<$<CONFIG:RELEASE>:/O2>")
endif (MSVC)
if (UNIX)
    # todo
endif (UNIX)
