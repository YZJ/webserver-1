CMAKE_MINIMUM_REQUIRED(VERSION 2.8.12)
PROJECT(webserver)

SET(CMAKE_VERBOSE_MAKEFILE ON)
SET(CMAKE_CXX_COMPILER g++)
ADD_COMPILE_OPTIONS("-Wall")
SET(WEBSERVER_SOURCES
	webserver/parse.cpp
	webserver/tinyhttp.cpp
	webserver/utility.cpp
)
ADD_EXECUTABLE(webserver ${WEBSERVER_SOURCES})
TARGET_LINK_LIBRARIES(webserver pthread)
ADD_CUSTOM_TARGET(debug
	COMMAND ${CMAKE_COMMAND} -DCMAKE_BUILD_TYPE=Debug ${CMAKE_SOURCE_DIR}
	COMMAND ${CMAKE_COMMAND} --build ${CMAKE_BINARY_DIR} --target all
	COMMENT "Switch CMAKE_BUILD_TYPE to Debug"

)
ADD_CUSTOM_TARGET(release
	COMMAND ${CMAKE_COMMAND} -DCMAKE_BUILD_TYPE=Release ${CMAKE_SOURCE_DIR}
	COMMAND ${CMAKE_COMMAND} --build ${CMAKE_BINARY_DIR} --target all
	COMMENT "Switch CMAKE_BUILD_TYPE to Release"
)
