cmake_minimum_required(VERSION 3.10)

#set(CMAKE_BUILD_TYPE debug)
set(CMAKE_BUILD_TYPE release)
#CMAKE_CXX_FLAGS_RELEASE = -O3 -DNDEBUG
SET(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O3")

set(CMAKE_CXX_STANDARD 17)
# Windows 系统下指定 pytorch 路径和 opencv 路径
# set(Torch_DIR /path/to/libtorch/share/cmake/Torch)
# set(OpenCV_DIR /path/to/opencv/build)

set(TORCH_PATH /home/an/project/libtorch/share/cmake/Torch)
if( TORCH_PATH )
    message("TORCH_PATH set to: ${TORCH_PATH}")
    set(Torch_DIR ${TORCH_PATH})
else()
    message(FATAL_ERROR "Need to specify Torch path, e.g., pytorch/torch/share/cmake/Torch ")
endif()


project(YoloLibTorch)

include_directories(./include)

add_subdirectory(./src)
add_subdirectory(./test)

install(TARGETS test Yolo
    RUNTIME DESTINATION ${CMAKE_SOURCE_DIR}/bin
    ARCHIVE DESTINATION ${CMAKE_SOURCE_DIR}/lib
)