cmake_minimum_required(VERSION 3.10)
project(kcore)

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

# Source files
set(KCORE_SOURCES
    src/kresult.c
    src/kdefer.c
    src/other.c
)

# Static library
add_library(kcore_static STATIC ${KCORE_SOURCES})
target_include_directories(kcore_static PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
    $<INSTALL_INTERFACE:include>
)
set_target_properties(kcore_static PROPERTIES
    VERSION 0.0.0
    PUBLIC_HEADER "src/kcore.h"
    OUTPUT_NAME kcore
)

# Shared library
add_library(kcore_shared SHARED ${KCORE_SOURCES})
target_include_directories(kcore_shared PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
    $<INSTALL_INTERFACE:include>
)
set_target_properties(kcore_shared PROPERTIES
    VERSION 0.0.0
    PUBLIC_HEADER "src/kcore.h"
    OUTPUT_NAME kcore
)

# Default alias (static by default for convenience)
add_library(kcore ALIAS kcore_static)

# Install both
install(TARGETS kcore_static kcore_shared
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
    PUBLIC_HEADER DESTINATION include
)
