# cmake_minimum_required(VERSION 3.5)
# project(yolopv2_ncnn)
# set(CMAKE_BUILD_TYPE Release)
# set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -pie -fPIE -fPIC -Wall")

# find_package(OpenCV REQUIRED)
# if (OpenCV_FOUND)
#     message(STATUS "OpenCV_LIBS: ${OpenCV_LIBS}")
#     message(STATUS "OpenCV_INCLUDE_DIRS: ${OpenCV_INCLUDE_DIRS}")
# else ()
#     message(FATAL_ERROR "opencv Not Found!")
# endif (OpenCV_FOUND)

# find_package(OpenMP REQUIRED)
# if (OPENMP_FOUND)
#     message("OPENMP FOUND")
#     set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
#     set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
#     set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
# else ()
#     message(FATAL_ERROR "OpenMP Not Found!")
# endif ()

# include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
# include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include/ncnn)
# link_directories(${CMAKE_CURRENT_SOURCE_DIR}/lib)

# add_executable(yolopv2_ncnn src/yolopv2.cpp)
# target_link_libraries(yolopv2_ncnn ncnn ${OpenCV_LIBS})


cmake_minimum_required(VERSION 3.5)

project(yolopv2_ncnn)

add_definitions(-std=c++11)
add_definitions("-Wall")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fno-builtin -fopenmp")


find_package(OpenCV REQUIRED)
find_package(Vulkan REQUIRED)

if(True)
    find_package(OpenMP)
    if(NOT TARGET OpenMP::OpenMP_CXX AND (OpenMP_CXX_FOUND OR OPENMP_FOUND))
        set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
        set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
    endif()
endif()

include_directories(${OpenCV_DIR}/include
                       /home/titan/Documents/ncnn/build/install/include/ncnn
                       /home/titan/Documents/ncnn/build/install/lib)    # change ncnn_root_dir to yours
link_directories(${OpenCV_DIR}/lib/
                         /home/titan/Documents/ncnn/build/install/lib)             # change ncnn_root_dir to yours

set(OpenCV_LIBS opencv_core 
                opencv_highgui 
                opencv_imgproc 
                opencv_imgcodecs 
                opencv_videoio)

add_executable(yolopv2_ncnn src/yolopv2.cpp)
target_link_libraries(yolopv2_ncnn ncnn glslang SPIRV OGLCompiler OSDependent Vulkan::Vulkan ${OpenCV_LIBS} -lpthread -lm )