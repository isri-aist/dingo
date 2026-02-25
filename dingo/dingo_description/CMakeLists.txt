cmake_minimum_required(VERSION 3.22)
project(dingo_description)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

if(NOT DEFINED ENV{ROS_VERSION})
  message(FATAL_ERROR "ROS_VERSION is not set in the environment")
endif()
find_package(ament_cmake REQUIRED)

set(DATA_INSTALL_FOLDER "${CMAKE_INSTALL_PREFIX}/share/${PROJECT_NAME}")

foreach(dir convex launch meshes models rsdf rviz urdf)
  if(IS_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/${dir}")
    install(DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/${dir}/"
            DESTINATION "${DATA_INSTALL_FOLDER}/${dir}")
  endif()
endforeach()

ament_package()
