cmake_minimum_required(VERSION 3.8)
project(bumperbot_controller)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(ament_cmake_python REQUIRED) #add for python
find_package(rclpy REQUIRED)      #dependecies mention here
find_package(rclcpp REQUIRED)
find_package(Eigen3 REQUIRED)

find_package(std_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(nav_msgs REQUIRED)
find_package(tf2 REQUIRED)
find_package(tf2_ros REQUIRED)


ament_python_install_package(${PROJECT_NAME})  #for declaring python scripts

include_directories(include)
include_directories(${EIGEN3_INCLUDE_DIR})
# when you add new folder write here to install!!!
add_executable(controller_cpp src/simple_controller.cpp)
ament_target_dependencies(controller_cpp rclcpp geometry_msgs std_msgs ${Eigen_LIBRARIES} sensor_msgs nav_msgs tf2 tf2_ros)
# target_include_directories(controller_cpp PUBLIC
#   $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
#   $<INSTALL_INTERFACE:include>
# )

install(
  DIRECTORY include/  
  DESTINATION include
)

install(
  TARGETS
  controller_cpp
  DESTINATION lib/${PROJECT_NAME}
)
install(
  DIRECTORY config launch   
  DESTINATION share/${PROJECT_NAME}
)

install(PROGRAMS
  ${PROJECT_NAME}/simple_controller.py
  ${PROJECT_NAME}/noisy_controller.py
  ${PROJECT_NAME}/waypoint_navigation.py

  DESTINATION lib/${PROJECT_NAME}

)


if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  set(ament_cmake_copyright_FOUND TRUE)
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
