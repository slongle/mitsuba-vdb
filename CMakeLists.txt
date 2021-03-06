CMAKE_MINIMUM_REQUIRED( VERSION 2.8.3 FATAL_ERROR )

PROJECT( vdbvolume )

# OpenVDB
FIND_PATH( OPENVDB_DIR REQUIRED )
SET( OPENVDB_INCLUDE_DIR "${OPENVDB_DIR}/include" )
SET( OPENVDB_LIBRARY_DIR "${OPENVDB_DIR}/lib" )

# TBB
FIND_PATH( TBB_DIR REQUIRED )
SET( TBB_INCLUDE_DIR "${TBB_DIR}/include" )
SET( TBB_LIBRARY_DIR "${TBB_DIR}/lib" )

# Mitsuba & Dependencies
FIND_PATH( MITSUBA_DIR REQUIRED )
SET( MITSUBA_SDK_INCLUDE_DIR "${MITSUBA_DIR}/dist/sdk/include" )
SET( MITSUBA_SDK_LIBRARY_DIR "${MITSUBA_DIR}/dist/sdk/lib" )
SET( MITSUBA_DEPENDENCIES_INCLUDE_DIR "${MITSUBA_DIR}/dependencies/include" )
SET( MITSUBA_DEPENDENCIES_LIBRARY_DIR "${MITSUBA_DIR}/dependencies/lib/x64_vc10" )

INCLUDE_DIRECTORIES( ${MITSUBA_SDK_INCLUDE_DIR} ${MITSUBA_DEPENDENCIES_INCLUDE_DIR} ${OPENVDB_INCLUDE_DIR} ${TBB_INCLUDE_DIR} )
LINK_DIRECTORIES( ${MITSUBA_SDK_LIBRARY_DIR} ${MITSUBA_DEPENDENCIES_LIBRARY_DIR} ${OPENVDB_LIBRARY_DIR} ${TBB_LIBRARY_DIR} )

ADD_DEFINITIONS( -DSINGLE_PRECISION -DSPECTRUM_SAMPLES=3 -DMTS_BUILD_MODULE=2 )
ADD_LIBRARY( vdbvolume SHARED vdbvolume.cpp vdbvolume.h )
TARGET_LINK_LIBRARIES( vdbvolume openvdb tbb mitsuba-core mitsuba-render )
