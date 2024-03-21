cmake_minimum_required(VERSION 3.8)
project(ik_interfaces)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# Find dependencies
find_package(ament_cmake REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(rclcpp REQUIRED)



rosidl_generate_interfaces(${PROJECT_NAME}
  "msg/JointState.msg"
  "srv/CalcIK.srv"
  DEPENDENCIES builtin_interfaces geometry_msgs
  )
# keine änderung 
# # We add it to be able to use other modules of the scripts folder
# install(DIRECTORY
#   ik_interfaces
#   src
#   DESTINATION share/${PROJECT_NAME}
# )

install(
  DIRECTORY "srv"
  DESTINATION share/${PROJECT_NAME}
)

install(
  DIRECTORY "msg"
  DESTINATION share/${PROJECT_NAME}
)

# install(
#   DIRECTORY include/
#   DESTINATION include
# )


ament_export_dependencies(
  rosidl_default_runtime 
  geometry_msgs
  )

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()



