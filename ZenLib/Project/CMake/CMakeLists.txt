project(zenlib)

cmake_minimum_required(VERSION 2.8)

set(zenlib_SOURCES_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../../../ZenLib/Source)

include_directories(${zenlib_SOURCES_PATH})

add_definitions(-DUNICODE)

set(zenlib_HDRS
  ${zenlib_SOURCES_PATH}/ZenLib/BitStream.h
  ${zenlib_SOURCES_PATH}/ZenLib/BitStream_Fast.h
  ${zenlib_SOURCES_PATH}/ZenLib/BitStream_LE.h
  ${zenlib_SOURCES_PATH}/ZenLib/Conf.h
  ${zenlib_SOURCES_PATH}/ZenLib/Conf_Internal.h
  ${zenlib_SOURCES_PATH}/ZenLib/CriticalSection.h
  ${zenlib_SOURCES_PATH}/ZenLib/Dir.h
  ${zenlib_SOURCES_PATH}/ZenLib/File.h
  ${zenlib_SOURCES_PATH}/ZenLib/FileName.h
  ${zenlib_SOURCES_PATH}/ZenLib/Format/Html/Html_Handler.h
  ${zenlib_SOURCES_PATH}/ZenLib/Format/Html/Html_Request.h
  ${zenlib_SOURCES_PATH}/ZenLib/Format/Http/Http_Cookies.h
  ${zenlib_SOURCES_PATH}/ZenLib/Format/Http/Http_Handler.h
  ${zenlib_SOURCES_PATH}/ZenLib/Format/Http/Http_Request.h
  ${zenlib_SOURCES_PATH}/ZenLib/Format/Http/Http_Utils.h
  ${zenlib_SOURCES_PATH}/ZenLib/HTTP_Client.h
  ${zenlib_SOURCES_PATH}/ZenLib/HTTP_Client/HTTPClient.h
  ${zenlib_SOURCES_PATH}/ZenLib/HTTP_Client/HTTPClientAuth.h
  ${zenlib_SOURCES_PATH}/ZenLib/HTTP_Client/HTTPClientCommon.h
  ${zenlib_SOURCES_PATH}/ZenLib/HTTP_Client/HTTPClientString.h
  ${zenlib_SOURCES_PATH}/ZenLib/HTTP_Client/HTTPClientWrapper.h
  ${zenlib_SOURCES_PATH}/ZenLib/InfoMap.h
  ${zenlib_SOURCES_PATH}/ZenLib/MemoryDebug.h
  ${zenlib_SOURCES_PATH}/ZenLib/OS_Utils.h
  ${zenlib_SOURCES_PATH}/ZenLib/PreComp.h
  ${zenlib_SOURCES_PATH}/ZenLib/Thread.h
  ${zenlib_SOURCES_PATH}/ZenLib/Trace.h
  ${zenlib_SOURCES_PATH}/ZenLib/Translation.h
  ${zenlib_SOURCES_PATH}/ZenLib/Utils.h
  ${zenlib_SOURCES_PATH}/ZenLib/Ztring.h
  ${zenlib_SOURCES_PATH}/ZenLib/ZtringList.h
  ${zenlib_SOURCES_PATH}/ZenLib/ZtringListList.h
  ${zenlib_SOURCES_PATH}/ZenLib/ZtringListListF.h
  ${zenlib_SOURCES_PATH}/ZenLib/int128s.h
  ${zenlib_SOURCES_PATH}/ZenLib/int128u.h
)

set(zenlib_SRCS
	${zenlib_SOURCES_PATH}/ZenLib/Conf.cpp
	${zenlib_SOURCES_PATH}/ZenLib/CriticalSection.cpp
	${zenlib_SOURCES_PATH}/ZenLib/Dir.cpp
	${zenlib_SOURCES_PATH}/ZenLib/File.cpp
	${zenlib_SOURCES_PATH}/ZenLib/FileName.cpp
	${zenlib_SOURCES_PATH}/ZenLib/HTTP_Client.cpp
	${zenlib_SOURCES_PATH}/ZenLib/InfoMap.cpp
	${zenlib_SOURCES_PATH}/ZenLib/int128s.cpp
	${zenlib_SOURCES_PATH}/ZenLib/int128u.cpp
	${zenlib_SOURCES_PATH}/ZenLib/MemoryDebug.cpp
	${zenlib_SOURCES_PATH}/ZenLib/OS_Utils.cpp
	${zenlib_SOURCES_PATH}/ZenLib/Translation.cpp
	${zenlib_SOURCES_PATH}/ZenLib/Thread.cpp
	${zenlib_SOURCES_PATH}/ZenLib/Utils.cpp
	${zenlib_SOURCES_PATH}/ZenLib/Ztring.cpp
	${zenlib_SOURCES_PATH}/ZenLib/ZtringList.cpp
	${zenlib_SOURCES_PATH}/ZenLib/ZtringListList.cpp
	${zenlib_SOURCES_PATH}/ZenLib/ZtringListListF.cpp
	${zenlib_SOURCES_PATH}/ZenLib/Format/Html/Html_Handler.cpp
	${zenlib_SOURCES_PATH}/ZenLib/Format/Html/Html_Request.cpp
	${zenlib_SOURCES_PATH}/ZenLib/Format/Http/Http_Cookies.cpp
	${zenlib_SOURCES_PATH}/ZenLib/Format/Http/Http_Handler.cpp
	${zenlib_SOURCES_PATH}/ZenLib/Format/Http/Http_Request.cpp
	${zenlib_SOURCES_PATH}/ZenLib/Format/Http/Http_Utils.cpp
)

add_library(zenlib STATIC ${zenlib_SRCS} ${zenlib_HDRS})

install(TARGETS zenlib
  RUNTIME DESTINATION bin
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib )

foreach(HEADER ${zenlib_HDRS})
  string(REPLACE ${zenlib_SOURCES_PATH} "" DIR ${HEADER})
  string(REGEX REPLACE "/[^/]*$" "" DIR ${DIR})
  install(FILES ${HEADER} DESTINATION include/${DIR})
endforeach(HEADER ${zenlib_HDRS})
