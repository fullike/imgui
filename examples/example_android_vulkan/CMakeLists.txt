cmake_minimum_required(VERSION 3.6)

project(ImGuiExample)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -DVK_USE_PLATFORM_ANDROID_KHR -DVK_NO_PROTOTYPES")

add_library(${CMAKE_PROJECT_NAME} SHARED
  ${CMAKE_CURRENT_SOURCE_DIR}/main.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/../../imgui.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/../../imgui_demo.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/../../imgui_draw.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/../../imgui_tables.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/../../imgui_widgets.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/../../backends/imgui_impl_android.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/../../backends/imgui_impl_vulkan.cpp
  ${ANDROID_NDK}/sources/android/native_app_glue/android_native_app_glue.c
        ${ANDROID_NDK}/sources/third_party/vulkan/src/common/vulkan_wrapper.cpp
)

set(CMAKE_SHARED_LINKER_FLAGS
  "${CMAKE_SHARED_LINKER_FLAGS} -u ANativeActivity_onCreate"
)

target_compile_definitions(${CMAKE_PROJECT_NAME} PRIVATE
  IMGUI_IMPL_OPENGL_ES3
)

target_include_directories(${CMAKE_PROJECT_NAME} PRIVATE
  ${CMAKE_CURRENT_SOURCE_DIR}/../..
  ${CMAKE_CURRENT_SOURCE_DIR}/../../backends
  ${ANDROID_NDK}/sources/android/native_app_glue
        ${ANDROID_NDK}/sources/third_party/vulkan/src/include
        ${ANDROID_NDK}/sources/third_party/vulkan/src/common


)

target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE
  android
  EGL
  GLESv3
  log
)
