project(ZenLib)

cmake_minimum_required(VERSION 2.8.11)

if(WIN32)
  set(BUILD_SHARED_LIBS OFF)
endif()

option(ENABLE_UNICODE "Enable unicode support" ON)

set(ZenLib_SOURCES_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../../../ZenLib/Source)

set(ZenLib_MAJOR_VERSION "0")
set(ZenLib_MINOR_VERSION "4")
set(ZenLib_PATCH_VERSION "29")

set(ZenLib_VERSION_STRING "${ZenLib_MAJOR_VERSION}.${ZenLib_MINOR_VERSION}.${ZenLib_PATCH_VERSION}")

# On Windows debug library should have 'd' postfix.
if(WIN32)
  set(CMAKE_DEBUG_POSTFIX "d")
elseif(APPLE)
  set(CMAKE_DEBUG_POSTFIX "_debug")
endif()

set(LIB_SUFFIX "" CACHE STRING "Define suffix of directory name (32/64)" )
set(BIN_INSTALL_DIR "${CMAKE_INSTALL_PREFIX}/bin" CACHE STRING "Directory where binary will install")
set(LIB_INSTALL_DIR "${CMAKE_INSTALL_PREFIX}/lib${LIB_SUFFIX}" CACHE STRING "Directory where library will install")
set(INCLUDE_INSTALL_DIR "${CMAKE_INSTALL_PREFIX}/include" CACHE PATH "The directory the headers are installed in")

if(NOT MSVC)
  set(ZenLib_CONFIG_INSTALL_DIR "${LIB_INSTALL_DIR}/cmake/zenlib")
else()
  set(ZenLib_CONFIG_INSTALL_DIR "${CMAKE_INSTALL_PREFIX}/cmake/")
endif()

set(ZenLib_HDRS
  ${ZenLib_SOURCES_PATH}/ZenLib/BitStream.h
  ${ZenLib_SOURCES_PATH}/ZenLib/BitStream_Fast.h
  ${ZenLib_SOURCES_PATH}/ZenLib/BitStream_LE.h
  ${ZenLib_SOURCES_PATH}/ZenLib/Conf.h
  ${ZenLib_SOURCES_PATH}/ZenLib/Conf_Internal.h
  ${ZenLib_SOURCES_PATH}/ZenLib/CriticalSection.h
  ${ZenLib_SOURCES_PATH}/ZenLib/Dir.h
  ${ZenLib_SOURCES_PATH}/ZenLib/File.h
  ${ZenLib_SOURCES_PATH}/ZenLib/FileName.h
  ${ZenLib_SOURCES_PATH}/ZenLib/Format/Html/Html_Handler.h
  ${ZenLib_SOURCES_PATH}/ZenLib/Format/Html/Html_Request.h
  ${ZenLib_SOURCES_PATH}/ZenLib/Format/Http/Http_Cookies.h
  ${ZenLib_SOURCES_PATH}/ZenLib/Format/Http/Http_Handler.h
  ${ZenLib_SOURCES_PATH}/ZenLib/Format/Http/Http_Request.h
  ${ZenLib_SOURCES_PATH}/ZenLib/Format/Http/Http_Utils.h
  ${ZenLib_SOURCES_PATH}/ZenLib/HTTP_Client.h
  ${ZenLib_SOURCES_PATH}/ZenLib/HTTP_Client/HTTPClient.h
  ${ZenLib_SOURCES_PATH}/ZenLib/HTTP_Client/HTTPClientAuth.h
  ${ZenLib_SOURCES_PATH}/ZenLib/HTTP_Client/HTTPClientCommon.h
  ${ZenLib_SOURCES_PATH}/ZenLib/HTTP_Client/HTTPClientString.h
  ${ZenLib_SOURCES_PATH}/ZenLib/HTTP_Client/HTTPClientWrapper.h
  ${ZenLib_SOURCES_PATH}/ZenLib/InfoMap.h
  ${ZenLib_SOURCES_PATH}/ZenLib/MemoryDebug.h
  ${ZenLib_SOURCES_PATH}/ZenLib/OS_Utils.h
  ${ZenLib_SOURCES_PATH}/ZenLib/PreComp.h
  ${ZenLib_SOURCES_PATH}/ZenLib/Thread.h
  ${ZenLib_SOURCES_PATH}/ZenLib/Trace.h
  ${ZenLib_SOURCES_PATH}/ZenLib/Translation.h
  ${ZenLib_SOURCES_PATH}/ZenLib/Utils.h
  ${ZenLib_SOURCES_PATH}/ZenLib/Ztring.h
  ${ZenLib_SOURCES_PATH}/ZenLib/ZtringList.h
  ${ZenLib_SOURCES_PATH}/ZenLib/ZtringListList.h
  ${ZenLib_SOURCES_PATH}/ZenLib/ZtringListListF.h
  ${ZenLib_SOURCES_PATH}/ZenLib/int128s.h
  ${ZenLib_SOURCES_PATH}/ZenLib/int128u.h
  )

set(ZenLib_SRCS
  ${ZenLib_SOURCES_PATH}/ZenLib/Conf.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/CriticalSection.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/Dir.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/File.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/FileName.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/HTTP_Client.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/InfoMap.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/int128s.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/int128u.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/MemoryDebug.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/OS_Utils.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/Translation.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/Thread.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/Utils.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/Ztring.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/ZtringList.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/ZtringListList.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/ZtringListListF.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/Format/Html/Html_Handler.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/Format/Html/Html_Request.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/Format/Http/Http_Cookies.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/Format/Http/Http_Handler.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/Format/Http/Http_Request.cpp
  ${ZenLib_SOURCES_PATH}/ZenLib/Format/Http/Http_Utils.cpp
  )

add_library(zen ${ZenLib_SRCS} ${ZenLib_HDRS})
if(ENABLE_UNICODE)
  target_compile_definitions(zen PUBLIC UNICODE)
endif()

try_compile(SIZE_T_IS_NOT_LONG ${CMAKE_CURRENT_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/size_t_is_long_check.cpp)
if(NOT SIZE_T_IS_NOT_LONG)
  target_compile_definitions(zen PUBLIC SIZE_T_IS_LONG)
endif()

target_include_directories(zen INTERFACE ${INCLUDE_INSTALL_DIR})
target_include_directories(zen PRIVATE ${ZenLib_SOURCES_PATH})

set_target_properties(zen PROPERTIES
  VERSION ${ZenLib_MAJOR_VERSION}.${ZenLib_MINOR_VERSION}.${ZenLib_PATCH_VERSION}
  SOVERSION ${ZenLib_MAJOR_VERSION}
  )

if(MSVC)
  get_target_property(LOCATION zen LOCATION_DEBUG)
  string(REGEX REPLACE "\\.[^.]*$" ".pdb" LOCATION "${LOCATION}")
  install(FILES ${LOCATION} DESTINATION ${BIN_INSTALL_DIR} CONFIGURATIONS Debug)
  
  get_target_property(LOCATION zen LOCATION_RELWITHDEBINFO)
  string(REGEX REPLACE "\\.[^.]*$" ".pdb" LOCATION "${LOCATION}")
  install(FILES ${LOCATION} DESTINATION ${BIN_INSTALL_DIR} CONFIGURATIONS RelWithDebInfo)
endif()

install(TARGETS zen EXPORT zen-export
  RUNTIME DESTINATION ${BIN_INSTALL_DIR}
  ARCHIVE DESTINATION ${LIB_INSTALL_DIR}
  LIBRARY DESTINATION ${LIB_INSTALL_DIR})

install(EXPORT zen-export DESTINATION ${ZenLib_CONFIG_INSTALL_DIR} FILE ZenLibTargets.cmake)

foreach(HEADER ${ZenLib_HDRS})
  string(REPLACE ${ZenLib_SOURCES_PATH} "" DIR ${HEADER})
  string(REGEX REPLACE "/[^/]*$" "" DIR ${DIR})
  install(FILES ${HEADER} DESTINATION include/${DIR})
endforeach()

configure_file(
  "${CMAKE_CURRENT_SOURCE_DIR}/cmake_uninstall.cmake.in"
  "${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake"
  IMMEDIATE @ONLY)

# cmake-modules
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/ZenLibConfig.cmake.in
  ${CMAKE_CURRENT_BINARY_DIR}/ZenLibConfig.cmake
  @ONLY)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/ZenLibConfigVersion.cmake.in
  ${CMAKE_CURRENT_BINARY_DIR}/ZenLibConfigVersion.cmake
  @ONLY)

install(FILES 
  ${CMAKE_CURRENT_BINARY_DIR}/ZenLibConfig.cmake
  ${CMAKE_CURRENT_BINARY_DIR}/ZenLibConfigVersion.cmake
  DESTINATION ${ZenLib_CONFIG_INSTALL_DIR})

if(NOT TARGET uninstall)
  add_custom_target(uninstall
    "${CMAKE_COMMAND}" -P "${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake")
endif()
