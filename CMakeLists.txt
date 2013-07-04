cmake_minimum_required(VERSION 2.8.3)
project(openni_tracker)
find_package(catkin REQUIRED COMPONENTS geometry_msgs
					orocos_kdl
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
		    ${Nite_INCLUDEDIR})
add_executable(openni_tracker src/openni_tracker.cpp)
target_link_libraries(openni_tracker ${catkin_LIBRARIES} ${OpenNI_LIBRARIES} ${Nite_LIBRARY})

install(TARGETS openni_tracker RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
install(FILES openni_tracker.xml DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})
