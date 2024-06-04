cmake_minimum_required(VERSION 3.0.0)

project(CStudy)

include_directories(${PROJECT_SOURCE_DIR}/include)
set(CStudy_LIBRARIES CStudy)
message(STATUS "${PROJECT_SOURCE_DIR}")

# requires at least C++14
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wl,--exclude-libs,ALL")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -march=native")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O2")

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Debug")
endif()
message("CMAKE_BUILD_TYPE : " ${CMAKE_BUILD_TYPE})

# Eigen
find_package (Eigen3 3.3 REQUIRED NO_MODULE)
if(NOT ${Eigen3_FOUND})
    message("Eigen3 not found")
else()
    message("Found Eigen3!")
endif()

# 查找 VTK 库
if(NOT VTK_DIR)
    set(VTK_DIR "~/.local/vtk/lib/cmake/vtk-9.2")
endif()
find_package(VTK)
if(NOT ${VTK_FOUND})
    message("VTK not found")
else()
    message("Found vtk! ${VTK_USE_FILE}")
endif()

##################### Link to CGAL  #####################
if(NOT CGAL_DIR)
    set(CGAL_DIR "~/.local/cgal/lib/cmake/CGAL")
endif()
set(CGAL_DO_NOT_WARN_ABOUT_CMAKE_BUILD_TYPE TRUE)
find_package(CGAL)
if(NOT ${CGAL_FOUND})
    message("CGAL not found")
else()
    include_directories(${CGAL_INCLUDE_DIRS})
    message("Found cgal! ${CGAL_INCLUDE_DIRS}")
endif()

##################### Link to MFEM  #####################
if(NOT MFEM_DIR)
    set(MFEM_DIR "~/.local/mfem/lib/cmake/mfem")
endif()
find_package(MFEM)
if(NOT ${MFEM_FOUND})
    message("MFEM not found! in ${MFEM_DIR}")
else()
    include_directories(${MFEM_INCLUDE_DIRS})
    message("Found MFEM! ${MFEM_INCLUDE_DIRS}")
    message("${MFEM_LIBRARIES}")
endif()

##################### Link to MUMPS #####################
find_path(MUMPS_INCLUDE_DIR dmumps_c.h
    )
find_library(MUMPS_LIBRARY dmumps
    )
if(MUMPS_INCLUDE_DIR)
  if(MUMPS_LIBRARY)
    set(MUMPS_LIBRARIES ${MUMPS_LIBRARY})
    set(MUMPS_FOUND TRUE )
  endif()
endif()

if(NOT ${MUMPS_FOUND})
    message("MUMPS not found")
else()
    include_directories(${MUMPS_INCLUDE_DIR})
    message("Found MUMPS! ${MUMPS_INCLUDE_DIR}")
    message("Found MUMPS! ${MUMPS_LIBRARY}")
endif()

add_subdirectory(test)


