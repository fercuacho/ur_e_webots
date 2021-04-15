cmake_minimum_required(VERSION 3.16)

project(ur_e_webots)

find_package(catkin REQUIRED
  COMPONENTS
  actionlib
  actionlib_msgs
  std_msgs
)

catkin_python_setup()

add_action_files(
  FILES
  Attach.action
)

generate_messages(
  DEPENDENCIES
  actionlib_msgs
  std_msgs
)

catkin_package()

install(DIRECTORY launch DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})

catkin_install_python(PROGRAMS src/ur_e_webots/joint_state_publisher.py
  DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})

install(FILES
  launch/ur5e_webots.launch
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

install(FILES
  worlds/ur5e.wbt
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

if (CATKIN_ENABLE_TESTING)
  find_package(roslaunch REQUIRED)
  roslaunch_add_file_check(tests/roslaunch_test.xml)
endif()

