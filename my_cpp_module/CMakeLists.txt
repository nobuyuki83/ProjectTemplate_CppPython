cmake_minimum_required(VERSION 3.12)

#########################################################

enable_language(CXX)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)
if(MSVC)
  set(CMAKE_CXX_FLAGS "/W4 -O2 \
    /wd4530 /wd4577 /wd4100 /wd4458 /wd4244 /wd4702 /wd4996 \
    /wd4701 /wd4267 /wd4305 /wd4389 /wd4456 /wd4505 ")
else()
  set(CMAKE_CXX_FLAGS "-O2 -Wall -Wextra \
    -Wno-deprecated-declarations \
    -Wno-unused-parameter \
    -Wno-unused-function")
endif()

##########################################################

project(c_)

set(PYBIND11_DIR        "../pybind11")
add_subdirectory(${PYBIND11_DIR} pybind11)

########################

include_directories(
)

set(INPUT_SRC
    main.cpp
)

###########################################

pybind11_add_module(${PROJECT_NAME}
  ${INPUT_SRC} )

#target_link_libraries(${PROJECT_NAME}
#  PRIVATE ${INPUT_LIBRARY})

file(TO_NATIVE_PATH "${PROJECT_BINARY_DIR}" NATIVE_PROJECT_BINARY_DIR)
file(TO_NATIVE_PATH "${PROJECT_SOURCE_DIR}" NATIVE_PROJECT_SOURCE_DIR)

if(WIN32)
  add_custom_command(TARGET ${PROJECT_NAME}
  POST_BUILD
    COMMAND copy 
      "${NATIVE_PROJECT_BINARY_DIR}\\${CMAKE_CFG_INTDIR}\\${PROJECT_NAME}.*.pyd"   
      ${NATIVE_PROJECT_SOURCE_DIR}\\
    COMMENT "Post Event"
  )
else()
  add_custom_command(TARGET ${PROJECT_NAME}
  POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy 
      ${PROJECT_BINARY_DIR}/${CMAKE_CFG_INTDIR}/${PROJECT_NAME}.*
      ${PROJECT_SOURCE_DIR}/
    COMMENT "Post Event"
  )
endif()
