cmake_minimum_required(VERSION 2.4.6)
project(cyberglove)

find_package(catkin REQUIRED COMPONENTS
	cmake_modules
	rospy
	roslib
	roscpp
	sensor_msgs
	std_msgs
	diagnostic_msgs
)

find_package(TinyXML REQUIRED)

catkin_package(
	INCLUDE_DIRS include
	LIBRARIES serial_glove
	CATKIN_DEPENDS rospy roscpp roslib sensor_msgs diagnostic_msgs std_msgs
)

include_directories(
	include
	${TinyXML_INCLUDE_DIRS}
	${catkin_INCLUDE_DIRS}
)

add_library(serial_glove src/serial_glove.c)

add_executable(cyberglove src/cyberglove_publisher.cpp src/cyberglove_node.cpp)
target_link_libraries(cyberglove serial_glove ${catkin_LIBRARIES} ${TinyXML_LIBRARIES})
