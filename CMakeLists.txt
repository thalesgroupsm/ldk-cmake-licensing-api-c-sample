#CMakeLists file

cmake_minimum_required (VERSION 3.0.0)

project (licensing_api_demo)

add_executable (hasp_demo src/hasp_demo.c)
add_executable (hasp_update src/hasp_update.c)
add_executable (hasp_admin_demo src/sntl_admin_demo.c)

target_include_directories(hasp_demo PUBLIC "${PROJECT_SOURCE_DIR}/inc")
target_include_directories(hasp_update PUBLIC "${PROJECT_SOURCE_DIR}/inc")
target_include_directories(hasp_admin_demo PUBLIC "${PROJECT_SOURCE_DIR}/inc")

# point to included file and add library for Windows
if(CMAKE_SYSTEM_NAME STREQUAL "Windows")
	target_link_libraries(hasp_demo "${PROJECT_SOURCE_DIR}/lib/libhasp_windows_x64_demo.lib")
	target_link_libraries(hasp_update "${PROJECT_SOURCE_DIR}/lib/libhasp_windows_x64_demo.lib")
	target_link_libraries(hasp_admin_demo "${PROJECT_SOURCE_DIR}/lib/libsntl_adminapi_windows_x64.lib")
endif()

if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
	target_link_libraries(hasp_demo "${PROJECT_SOURCE_DIR}/lib/libhasp_linux_x64_demo.a")
	target_link_libraries(hasp_update "${PROJECT_SOURCE_DIR}/lib/libhasp_linux_x64_demo.a")
	target_link_libraries(hasp_admin_demo "${PROJECT_SOURCE_DIR}/lib/libsntl_adminapi_linux_x64.a")
endif()

