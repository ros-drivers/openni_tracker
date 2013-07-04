cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

rosbuild_init()
rosbuild_make_distribution(0.1.3)

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)

include(FindPkgConfig)
pkg_check_modules(OPENNI libopenni)


include_directories(${OPENNI_INCLUDEDIR} /usr/include/nite)
rosbuild_add_executable(openni_tracker src/openni_tracker.cpp)
target_link_libraries(openni_tracker ${OPENNI_LIBRARIES})
