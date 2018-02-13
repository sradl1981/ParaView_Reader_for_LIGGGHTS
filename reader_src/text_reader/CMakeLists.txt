PROJECT(liggghts_reader)
CMAKE_MINIMUM_REQUIRED(VERSION 2.6)
FIND_PACKAGE(ParaView REQUIRED)
INCLUDE(${PARAVIEW_USE_FILE})
IF(${PARAVIEW_VERSION_FULL} VERSION_GREATER "4.0.1")
    MESSAGE(STATUS "liggghts_reader for Paraview version > 4.0.1")
    ADD_PARAVIEW_PLUGIN(liggghts_reader "1.0.1"
        SERVER_MANAGER_XML liggghts_reader.xml
        SERVER_MANAGER_SOURCES liggghts_reader.cxx
        REQUIRED_ON_SERVER)
ELSE()
    MESSAGE(SEND_ERROR "liggghts_reader for Paraview version <= 4.0.1 NOT supported")
ENDIF()        

