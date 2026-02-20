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

file(GLOB_RECURSE xacro_SRC "${CMAKE_CURRENT_SOURCE_DIR}/urdf/*.xacro")

# find_program(XACRO xacro REQUIRED)
# set(urdf_OUT "${CMAKE_CURRENT_SOURCE_DIR}/urdf/dingo.urdf")
# set(xacro_IN "${CMAKE_CURRENT_SOURCE_DIR}/urdf/dingo.urdf.xacro")
# message(STATUS "Generating URDF at ${urdf_OUT} from ${xacro_IN}")

# add_custom_command(
#   OUTPUT ${urdf_OUT}
#   COMMAND 
#     ${XACRO} ${xacro_IN} -o ${urdf_OUT}
#   DEPENDS ${xacro_SRC}
# COMMENT "Generate ${urdf_OUT}")

# add_custom_target(generate-dingo-urdf ALL DEPENDS ${urdf_OUT})
# add_dependencies(generate-dingo-urdf)

# foreach(dir convex launch meshes models rsdf rviz urdf)
#   if(IS_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/${dir}")
#     install(DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/${dir}/"
#             DESTINATION "${DATA_INSTALL_FOLDER}/${dir}")
#   endif()
# endforeach()

install(
  DIRECTORY launch meshes rsdf rviz urdf
  DESTINATION share/${PROJECT_NAME}
)

ament_package()
