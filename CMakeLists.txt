# http://ros.org/doc/groovy/api/catkin/html/user_guide/supposed.html
cmake_minimum_required(VERSION 2.8.3)
project(laserscan_to_pointcloud)

# Load catkin and all dependencies required for this package
# TODO: remove all from COMPONENTS that are not catkin packages.
find_package(catkin REQUIRED COMPONENTS roscpp laser_geometry laser_filters tf)

# include_directories(include ${Boost_INCLUDE_DIR} ${catkin_INCLUDE_DIRS})
# CATKIN_MIGRATION: removed during catkin migration
# cmake_minimum_required(VERSION 2.4.6)

# CATKIN_MIGRATION: removed during catkin migration
# include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE RelWithDebInfo)

catkin_package(
    DEPENDS
    CATKIN-DEPENDS roscpp laser_geometry laser_filters tf
    INCLUDE_DIRS ${Boost_INCLUDE_DIRS} ${catkin_INCLUDE_DIRS}
    LIBRARIES ${Boost_LIBRARIES} ${catkin_LIBRARIES}
)

include_directories(${Boost_INCLUDE_DIRS} ${catkin_INCLUDE_DIRS})

add_executable(laserscan_to_pointcloud_node src/laserscan_to_pointcloud_node.cpp)
target_link_libraries(laserscan_to_pointcloud_node ${Boost_LIBRARIES} ${catkin_LIBRARIES} )
add_dependencies(laserscan_to_pointcloud_node ${catkin_EXPORTED_TARGETS})

## Mark other files for installation (e.g. launch and bag files, etc.)
install(DIRECTORY launch config
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

install(TARGETS laserscan_to_pointcloud_node
        DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)