cmake_minimum_required(VERSION 3.11 FATAL_ERROR)

if(POLICY CMP0048)
    cmake_policy(SET CMP0048 NEW)
endif()


# -----------------------------------------------------------------------------
# Make RelWithDebInfo the default build type if otherwise not set
# -----------------------------------------------------------------------------
IF(DEFINED CMAKE_BUILD_TYPE)
  SET(CMAKE_BUILD_TYPE ${CMAKE_BUILD_TYPE}
  CACHE STRING "Choose the type of build: None(CMAKE_CXX_FLAGS or CMAKE_C_FLAGS used) Debug Release RelWithDebInfo MinSizeRel.")
ELSE()
  SET(CMAKE_BUILD_TYPE RelWithDebInfo CACHE STRING
  "Choose the type of build, options are: None(CMAKE_CXX_FLAGS or CMAKE_C_FLAGS used) Debug Release RelWithDebInfo MinSizeRel.")
ENDIF()

PROJECT(sha1-sat)

option(STATICCOMPILE "Compile to static executable" OFF)
if (STATICCOMPILE)
    set(BUILD_SHARED_LIBS OFF)
endif()


add_executable(sha1-gen
    main.cc
)

set_target_properties(sha1-gen PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}
    INSTALL_RPATH_USE_LINK_PATH TRUE)

target_link_libraries(sha1-gen
)

add_executable(sha1-verify
    verify-preimage.cc
)

