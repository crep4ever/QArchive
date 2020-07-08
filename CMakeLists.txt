# BSD-3 Clause.
# Copyright (C) 2018 Antony Jr.
# -------------------------------
#  CMake Support for QArchive.
# -------------------------------

CMAKE_MINIMUM_REQUIRED( VERSION 3.2)
project(QArchive)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)

# Find the QtCore library.
find_package(Qt5 COMPONENTS Core REQUIRED)
list(APPEND LIBRARIES Qt5::Core)

# Find LibArchive
find_package(LibArchive REQUIRED)
list(APPEND LIBRARIES ${LibArchive_LIBRARIES})

# Include Directories.
include_directories(${CMAKE_CURRENT_LIST_DIR})
include_directories(${CMAKE_CURRENT_LIST_DIR}/include)

add_library(${PROJECT_NAME}
	    src/qarchivediskcompressor.cc
	    src/qarchivediskextractor.cc
	    src/qarchive_enums.cc
	    src/qarchivediskcompressor_p.cc
	    src/qarchivediskextractor_p.cc
	    src/qarchiveutils_p.cc
	    src/qarchiveioreader_p.cc
	    include/qarchivediskcompressor.hpp
	    include/qarchivediskextractor.hpp
	    include/qarchive_enums.hpp
	    include/qarchivediskcompressor_p.hpp
	    include/qarchivediskextractor_p.hpp
	    include/qarchiveutils_p.hpp
	    include/qarchiveioreader_p.hpp
	    )

target_link_libraries(${PROJECT_NAME} PUBLIC ${LIBRARIES})

target_include_directories(${PROJECT_NAME} PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
  $<INSTALL_INTERFACE:include>${CMAKE_CURRENT_SOURCE_DIR})
