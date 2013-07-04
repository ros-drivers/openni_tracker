cmake_minimum_required(VERSION 2.8.3)
project(openni_tracker)
#include(FindPkgConfig)
find_package(catkin REQUIRED COMPONENTS geometry_msgs
					kdl
					roscpp
					tf)
find_package(PkgConfig)
pkg_check_modules(OpenNI libopenni)

catkin_package()

include_directories(${catkin_INCLUDEDIR} ${OPENNI_INCLUDEDIR} /usr/include/nite)
add_executable(openni_tracker src/openni_tracker.cpp)
target_link_libraries(openni_tracker ${catkin_LIBRARIES} ${OpenNI_LIBRARIES})

install(TARGETS openni_tracker RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
install(FILES openni_tracker.xml DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})
