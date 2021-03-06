add_subdirectory(utils)
add_executable(${PROJECT_NAME} main.cpp)
target_sources(${PROJECT_NAME} PRIVATE
	           "${CMAKE_CURRENT_SOURCE_DIR}/engine.h"
			   "${CMAKE_CURRENT_SOURCE_DIR}/engine.cpp"
			   "${CMAKE_CURRENT_SOURCE_DIR}/game/game.h"
			   "${CMAKE_CURRENT_SOURCE_DIR}/game/game.cpp"
			   "${CMAKE_CURRENT_SOURCE_DIR}/game/world.h"
			   "${CMAKE_CURRENT_SOURCE_DIR}/game/world.cpp"
			   "${CMAKE_CURRENT_SOURCE_DIR}/game/world_renderer.cpp"
			   "${CMAKE_CURRENT_SOURCE_DIR}/game/world_renderer.h"
			   "${CMAKE_CURRENT_SOURCE_DIR}/system.h"
			   "${CMAKE_CURRENT_SOURCE_DIR}/graphics_manager.h"
			   "${CMAKE_CURRENT_SOURCE_DIR}/graphics_manager.cpp"
			   "${CMAKE_CURRENT_SOURCE_DIR}/assets.h"
			   "${CMAKE_CURRENT_SOURCE_DIR}/input_manager.h"
			   "${CMAKE_CURRENT_SOURCE_DIR}/input_manager.cpp"
			   "${CMAKE_CURRENT_SOURCE_DIR}/renderer/renderer.h"
			   "${CMAKE_CURRENT_SOURCE_DIR}/renderer/renderer.cpp"
			   "${CMAKE_CURRENT_SOURCE_DIR}/renderer/gl_renderer.h"
			   "${CMAKE_CURRENT_SOURCE_DIR}/renderer/gl_renderer.cpp"
			   "${CMAKE_CURRENT_SOURCE_DIR}/platform/platform.h"
			   "${CMAKE_CURRENT_SOURCE_DIR}/platform/platform.cpp"
			   "${CMAKE_CURRENT_SOURCE_DIR}/platform/sdl_platform.h"
			   "${CMAKE_CURRENT_SOURCE_DIR}/platform/sdl_platform.cpp"
			   "${CMAKE_CURRENT_SOURCE_DIR}/loaders/file.h"
			   "${CMAKE_CURRENT_SOURCE_DIR}/loaders/file.cpp"
			   "${CMAKE_CURRENT_SOURCE_DIR}/loaders/image_loader.h"
			   "${CMAKE_CURRENT_SOURCE_DIR}/loaders/image_loader.cpp"
			   "${CMAKE_CURRENT_SOURCE_DIR}/loaders/data_loader.h"
			   "${CMAKE_CURRENT_SOURCE_DIR}/loaders/data_loader.cpp")
target_compile_features(${PROJECT_NAME} PUBLIC cxx_std_17)
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

target_include_directories(${PROJECT_NAME} PRIVATE ${LIBEPOXY_INCLUDE_DIRS})

include(CheckIPOSupported)
check_ipo_supported(RESULT result OUTPUT output)
if(result)
  set_property(TARGET ${PROJECT_NAME} PROPERTY INTERPROCEDURAL_OPTIMIZATION_RELEASE TRUE)
endif()

target_compile_options(${PROJECT_NAME} PUBLIC "-fno-exceptions")
target_compile_options(${PROJECT_NAME} PUBLIC "-fno-rtti")

target_link_libraries(${PROJECT_NAME} PRIVATE utils PNG::PNG SDL2::SDL2 OpenGL::GL ${LIBEPOXY_LIBRARIES})

if(CMAKE_BUILD_TYPE STREQUAL "Debug")
	set_property(TARGET ${PROJECT_NAME} PROPERTY ENABLE_EXPORTS TRUE)
endif()
