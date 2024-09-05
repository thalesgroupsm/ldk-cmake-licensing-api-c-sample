#CMakeLists file

cmake_minimum_required (VERSION 3.0.0)

project (licensing_api_demo)

add_executable (hasp_demo src/hasp_demo.c)
add_executable (hasp_update src/hasp_update.c)

target_include_directories(hasp_demo PUBLIC "${PROJECT_SOURCE_DIR}/inc")
target_include_directories(hasp_update PUBLIC "${PROJECT_SOURCE_DIR}/inc")
	
# Point to included file and add library for Windows
# Note: CMake use Win32 as defualt platform generator
if(CMAKE_SYSTEM_NAME STREQUAL "Windows")
	if("${CMAKE_SYSTEM_PROCESSOR}" STREQUAL "AMD64")
		target_link_libraries(hasp_demo "${PROJECT_SOURCE_DIR}/lib/libhasp_windows_x64_demo.lib")
		target_link_libraries(hasp_update "${PROJECT_SOURCE_DIR}/lib/libhasp_windows_x64_demo.lib")
	else()
		target_link_libraries(hasp_demo "${PROJECT_SOURCE_DIR}/lib/libhasp_windows_demo.lib")
		target_link_libraries(hasp_update "${PROJECT_SOURCE_DIR}/lib/libhasp_windows_demo.lib")
	endif()
elseif(CMAKE_SYSTEM_NAME STREQUAL "Linux")
	set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -pthread")
	if(${CMAKE_SYSTEM_PROCESSOR} STREQUAL "x86_64")
		target_link_libraries(hasp_demo "${PROJECT_SOURCE_DIR}/lib/libhasp_linux_x86_64_demo.a")
		target_link_libraries(hasp_update "${PROJECT_SOURCE_DIR}/lib/libhasp_linux_x86_64_demo.a")
	elseif(${CMAKE_SYSTEM_PROCESSOR} STREQUAL "aarch64")
		target_link_libraries(hasp_demo "${PROJECT_SOURCE_DIR}/lib/libhasp_linux_arm64_demo.a")
		target_link_libraries(hasp_update "${PROJECT_SOURCE_DIR}/lib/libhasp_linux_arm64_demo.a")
	endif()
endif()

