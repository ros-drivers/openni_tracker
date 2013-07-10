cmake_minimum_required(VERSION 2.8.3)

project(openni_tracker)

find_package(orocos_kdl REQUIRED)
find_package(catkin REQUIRED COMPONENTS geometry_msgs
					roscpp
					roslib
					tf)
# Find OpenNI
find_package(PkgConfig)
pkg_check_modules(OpenNI REQUIRED libopenni)

# Find Nite
find_path(Nite_INCLUDEDIR
	  NAMES XnVNite.h
	  HINTS /usr/include/nite /usr/local/include/nite)
find_library(Nite_LIBRARY
	     NAMES XnVNite_1_3_1
	     HINTS /usr/lib /usr/local/lib
	     PATH_SUFFIXES lib) 

catkin_package()

include_directories(${catkin_INCLUDEDIR}
		    ${OpenNI_INCLUDEDIR}
		    ${Nite_INCLUDEDIR}
		    ${orocos_kdl_INCLUDE_DIRS})

link_directories(${catkin_LIBRARY_DIRS})
link_directories(${orocos_kdl_LIBRARY_DIRS})

add_executable(openni_tracker src/openni_tracker.cpp)

add_dependencies(openni_tracker geometry_msgs_gencpp)

target_link_libraries(openni_tracker ${catkin_LIBRARIES}
				     ${OpenNI_LIBRARIES}
				     ${Nite_LIBRARY}
				     ${orocos_kdl_LIBRARIES})

install(TARGETS openni_tracker RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
install(FILES openni_tracker.xml DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})
