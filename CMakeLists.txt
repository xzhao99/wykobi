cmake_minimum_required (VERSION 3.15)

project(wykobi LANGUAGES CXX )

# cmake -B .\build\ -DCMAKE_BUILD_TYPE=Debug
# 

add_executable(${PROJECT_NAME} wykobi_build.cpp)


target_include_directories(${PROJECT_NAME} PUBLIC "${CMAKE_SOURCE_DIR}/include")

# comment out
if (0)
  if(MSVC)
    if(${CMAKE_BUILD_TYPE} MATCHES "Debug")
      target_compile_options(${PROJECT_NAME} PRIVATE /W4 /WX)
    endif()
  else()
    if(${CMAKE_BUILD_TYPE} MATCHES "Debug")
      target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra -Wpedantic -Werror)
    endif()
  endif()
endif()

# a more concise way
target_compile_options(${PROJECT_NAME} PRIVATE
    $<$<CXX_COMPILER_ID:MSVC>: /W4 /WX>
    $<$<NOT:$<CXX_COMPILER_ID:MSVC>>: -Wall -Wextra -Wpedantic -Werror>
    )