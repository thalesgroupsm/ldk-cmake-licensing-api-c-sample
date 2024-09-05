#CMakeLists file

cmake_minimum_required (VERSION 3.0.0)

project (licensing_api_demo)

add_executable (hasp_demo src/hasp_demo.c)
add_executable (hasp_update src/hasp_update.c)
if(NOT ("${CMAKE_SYSTEM_NAME}" STREQUAL "Linux" AND NOT "${CMAKE_SYSTEM_PROCESSOR}" STREQUAL "x86_64"))
	add_executable (hasp_admin_demo src/sntl_admin_demo.c)
endif()

target_include_directories(hasp_demo PUBLIC "${PROJECT_SOURCE_DIR}/inc")
target_include_directories(hasp_update PUBLIC "${PROJECT_SOURCE_DIR}/inc")
# Admin API supports only x86_64 CPU
if(NOT ("${CMAKE_SYSTEM_NAME}" STREQUAL "Linux" AND NOT "${CMAKE_SYSTEM_PROCESSOR}" STREQUAL "x86_64"))
	target_include_directories(hasp_admin_demo PUBLIC "${PROJECT_SOURCE_DIR}/inc")
endif()
	
# Point to included file and add library for Windows
# Note: CMake use Win32 as defualt platform generator
if(CMAKE_SYSTEM_NAME STREQUAL "Windows")
if(("${CMAKE_SYSTEM_PROCESSOR}" STREQUAL "AMD64" OR "${CMAKE_GENERATOR_PLATFORM}" STREQUAL "Win64") AND NOT "${CMAKE_GENERATOR_PLATFORM}" STREQUAL "")
	target_link_libraries(hasp_demo "${PROJECT_SOURCE_DIR}/lib/libhasp_windows_x64_demo.lib")
	target_link_libraries(hasp_update "${PROJECT_SOURCE_DIR}/lib/libhasp_windows_x64_demo.lib")
	target_link_libraries(hasp_admin_demo "${PROJECT_SOURCE_DIR}/lib/libsntl_adminapi_windows_x64.lib")
else()
	target_link_libraries(hasp_demo "${PROJECT_SOURCE_DIR}/lib/libhasp_windows_demo.lib")
	target_link_libraries(hasp_update "${PROJECT_SOURCE_DIR}/lib/libhasp_windows_demo.lib")
	target_link_libraries(hasp_admin_demo "${PROJECT_SOURCE_DIR}/lib/libsntl_adminapi_windows.lib")
endif()
endif()

if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -pthread")
if(${CMAKE_SYSTEM_PROCESSOR} STREQUAL "x86_64")
	target_link_libraries(hasp_demo "${PROJECT_SOURCE_DIR}/lib/libhasp_linux_x86_64_demo.a")
	target_link_libraries(hasp_update "${PROJECT_SOURCE_DIR}/lib/libhasp_linux_x86_64_demo.a")
	target_link_libraries(hasp_admin_demo "${PROJECT_SOURCE_DIR}/lib/libsntl_adminapi_linux_x86_64.a")
elseif(${CMAKE_SYSTEM_PROCESSOR} MATCHES "arm*" OR ${CMAKE_SYSTEM_PROCESSOR} STREQUAL "aarch64")
	target_link_libraries(hasp_demo "${PROJECT_SOURCE_DIR}/lib/libhasp_linux_arm64_demo.a")
	target_link_libraries(hasp_update "${PROJECT_SOURCE_DIR}/lib/libhasp_linux_arm64_demo.a")
	message(STATUS "hasp_admin_demo is not supported on Linux ARM")
endif()
endif()

