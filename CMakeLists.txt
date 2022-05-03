file(GLOB ImGui_SOURCES *.cpp)
file(GLOB ImGui_HEADERS *.h)

list(APPEND ImGui_HEADERS "backends/imgui_impl_glfw.h"
     "backends/imgui_impl_vulkan.h"
)

list(APPEND ImGui_SOURCES "backends/imgui_impl_glfw.cpp"
     "backends/imgui_impl_vulkan.cpp"
)

include(FindVulkan)
if(NOT Vulkan_FOUND)
  log_fatal("Vulkan NOT FOUND! Vulkan Tutorial requires a Vulkan SDK")
endif()

add_library(imgui)
target_sources(imgui PUBLIC ${ImGui_SOURCES})
target_include_directories(
  imgui PUBLIC ${CMAKE_CURRENT_LIST_DIR} ${CMAKE_CURRENT_LIST_DIR}/backends
               ${Vulkan_INCLUDE_DIR}
)
target_link_libraries(imgui PUBLIC YAGEN::glfw)
