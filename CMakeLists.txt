cmake_minimum_required(VERSION 3.0)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

set (PROJECT_NAME luapanda_luasocket)

project(${PROJECT_NAME} VERSION 1.0)

set (LIB_LUA lua53)
set (LIB_LUA_PATH lua-5.3.5/src)

include_directories(${LIB_LUA_PATH})


file(GLOB_RECURSE LUA_SOURCES "${LIB_LUA_PATH}/*.cpp" "${LIB_LUA_PATH}/*.c" "${LIB_LUA_PATH}/*.h" "${LIB_LUA_PATH}/*.inc")


#Generate the static library from the sources
add_library(${LIB_LUA} STATIC ${LUA_SOURCES}) 
set_target_properties(${LIB_LUA} PROPERTIES LINKER_LANGUAGE C)

set (LIB_LUA_SOCKET luasocket)
set (LIB_LUASOCKET_PATH luasocket/src)
#file(GLOB_RECURSE LUA_SOCKET_SOURCES "${LIB_LUASOCKET_PATH}/*.cpp" "${LIB_LUASOCKET_PATH}/*.c" "${LIB_LUASOCKET_PATH}/*.h" "${LIB_LUASOCKET_PATH}/*.inc")
set (LUA_SOCKET_SOURCES ${LIB_LUASOCKET_PATH}/auxiliar.c 
	${LIB_LUASOCKET_PATH}/buffer.c 
	${LIB_LUASOCKET_PATH}/except.c 
	${LIB_LUASOCKET_PATH}/inet.c 
	${LIB_LUASOCKET_PATH}/io.c 
	${LIB_LUASOCKET_PATH}/luasocket.c 
	${LIB_LUASOCKET_PATH}/options.c 
	${LIB_LUASOCKET_PATH}/select.c 
	${LIB_LUASOCKET_PATH}/tcp.c 
	${LIB_LUASOCKET_PATH}/timeout.c 
	${LIB_LUASOCKET_PATH}/udp.c 
	${LIB_LUASOCKET_PATH}/wsocket.c 
	${LIB_LUASOCKET_PATH}/mime.c)


#Generate the shared library from the sources
add_library(${LIB_LUA_SOCKET} SHARED ${LUA_SOCKET_SOURCES})
target_link_libraries ( ${LIB_LUA_SOCKET} ${LIB_LUA} Ws2_32 )
set_target_properties(${LIB_LUA_SOCKET} PROPERTIES LINKER_LANGUAGE CXX)
