cmake_minimum_required (VERSION 3.10)

set(PROJECT_NAME "VulkanTest")
project (${PROJECT_NAME})
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Vulkan SDK
set(VK_SDK_PATH "D:/Softwares/VulkanSDK/1.4.328.1")
set(VK_SDK_INCLUDE ${VK_SDK_PATH}/Include)
set(VK_SDK_LIB ${VK_SDK_PATH}/Lib/vulkan-1.lib)

# glm and glfw3
set(GLM_PATH "D:/Tools/glm/glm-1.0.2")
set(GLM_INCLUDE ${GLM_PATH})

set(GLFW_PATH "D:/Tools/glfw/glfw-3.4")
set(GLFW_INCLUDE "${GLFW_PATH}/include")
set(GLFW_LIBRARY  "${GLFW_PATH}/lib-vc2022/glfw3.lib")

file(GLOB_RECURSE HEADER_FILES ${PROJECT_SOURCE_DIR} "include/*.h")
file(GLOB_RECURSE SOURCE_FILES ${PROJECT_SOURCE_DIR} "src/*.cpp")
file(GLOB_RECURSE SHADER_FILES ${PROJECT_SOURCE_DIR} "shaders/*.frag" "shaders/*.vert")

source_group(TREE "${CMAKE_CURRENT_SOURCE_DIR}" FILES ${HEADER_FILES} ${SOURCE_FILES} ${SHADER_FILES})
add_executable(${PROJECT_NAME} ${SOURCE_FILES} ${HEADER_FILES} ${SHADER_FILES})

# link
target_link_libraries(${PROJECT_NAME} PRIVATE 
    ${VK_SDK_LIB}
    ${GLFW_LIBRARY}
)

# include
target_include_directories(${PROJECT_NAME} PRIVATE ${PROJECT_SOURCE_DIR}/include)
target_include_directories(${PROJECT_NAME} PRIVATE ${PROJECT_SOURCE_DIR}/3dparty)
target_include_directories(${PROJECT_NAME} PRIVATE ${VK_SDK_INCLUDE})
target_include_directories(${PROJECT_NAME} PRIVATE ${GLM_PATH_INCLUDE})
target_include_directories(${PROJECT_NAME} PRIVATE ${GLFW_INCLUDE})

add_subdirectory(3dparty)