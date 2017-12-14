cmake_minimum_required(VERSION 2.8.3)
project(dwl_lcmtypes)


# Checking if the project is compiling with Catkin or CMake
set(CATKIN_CALL "${CATKIN_DEVEL_PREFIX}")
if(CATKIN_CALL)
	message("Compiling dwl_lcmtypes as a Catkin project")
	find_package(catkin REQUIRED)

	# Setting the output directories for libraries and executables
	set(INCLUDE_OUTPUT_PATH  ${CATKIN_DEVEL_PREFIX}/include)
	set(LIBRARY_OUTPUT_PATH  ${CATKIN_DEVEL_PREFIX}/lib)
    set(EXECUTABLE_OUTPUT_PATH  ${CATKIN_DEVEL_PREFIX}/bin)
	set(PKG_CONFIG_OUTPUT_PATH  ${CATKIN_DEVEL_PREFIX}/lib/pkgconfig)
else()
	message("Compiling dwl_lcmtypes as a CMake project")

	# Setting the output directories for libraries and executables
	set(CMAKE_LIBRARY_OUTPUT_DIRECTORY  ${CMAKE_SOURCE_DIR}/lib)
	set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY  ${CMAKE_SOURCE_DIR}/lib)
	set(CMAKE_RUNTIME_OUTPUT_DIRECTORY  ${CMAKE_SOURCE_DIR}/bin)
	set(INCLUDE_OUTPUT_PATH  ${CMAKE_SOURCE_DIR}/include)
	set(INCLUDE_OUTPUT_PATH  ${CMAKE_SOURCE_DIR}/include)
	set(LIBRARY_OUTPUT_PATH  ${CMAKE_SOURCE_DIR}/lib)
    set(EXECUTABLE_OUTPUT_PATH  ${CMAKE_SOURCE_DIR}/bin)
	set(PKG_CONFIG_OUTPUT_PATH  ${CMAKE_SOURCE_DIR}/lib/pkgconfig)
endif()

# Building the dwl lcmtypes using a script from bot_core_lcmtypes packages
set(POD_NAME dwl_lcmtypes)
include(cmake/pods.cmake)
include(cmake/lcmtypes.cmake)
lcmtypes_build(C_AGGREGATE_HEADER dwl_lcmtypes.h CPP_AGGREGATE_HEADER dwl_lcmtypes.hpp)

# Setting the thirdparties directories and libraries
set(DEPENDENCIES_INCLUDE_DIRS  ${LCM_INCLUDE_DIRS})
set(DEPENDENCIES_LIBRARIES  ${LCM_LIBRARIES})
set(DEPENDENCIES_LIBRARY_DIRS  ${LCM_LIBRARY_DIRS})

# Including directories
set(INCLUDE_DIRS  ${lcmtypes_gen_INCLUDE_DIRS})
include_directories(${INCLUDE_DIRS})

# Exporting the package for use from the build-tree
# (this registers the build-tree with a global CMake-registry)
export(PACKAGE dwl_lcmtypes)

# Adding the description of the dwl_lcmtypes packages
if(CATKIN_CALL)
	catkin_package(
		INCLUDE_DIRS ${INCLUDE_DIRS} ${DEPENDENCIES_INCLUDE_DIRS}
		LIBRARIES ${PROJECT_NAME})
else()
    # Installing catkin package.xml and dwl-config.cmake for dwl as pure cmake project
    install(FILES package.xml DESTINATION share/dwl_lcmtypes)
    install(FILES "${CMAKE_LIBRARY_OUTPUT_DIRECTORY}/cmake/dwl_lcmtypes/dwl_lcmtypes-config.cmake" DESTINATION share/dwl_lcmtypes/cmake)

	# Creating a dwl-config.cmake file for the use from the build tree
	set(DWL_LCMTYPES_INCLUDE_DIRS  ${INCLUDE_DIRS}
								   ${DEPENDENCIES_INCLUDE_DIRS})
	set(DWL_LCMTYPES_LIBRARY_DIRS  ${CMAKE_LIBRARY_OUTPUT_DIRECTORY}
								   ${DEPENDENCIES_LIBRARY_DIRS})
	set(DWL_LCMTYPES_LIBRARIES  ${CMAKE_LIBRARY_OUTPUT_DIRECTORY}/libdwl_lcmtypes${CMAKE_STATIC_LIBRARY_SUFFIX}
							    ${DEPENDENCIES_LIBRARIES})
	configure_file(dwl_lcmtypes-config.cmake.in
		"${CMAKE_LIBRARY_OUTPUT_DIRECTORY}/cmake/dwl_lcmtypes/dwl_lcmtypes-config.cmake" @ONLY)
endif()
