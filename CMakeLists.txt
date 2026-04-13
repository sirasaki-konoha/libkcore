project(libkcore)

add_library(libkcore SHARED
    src/kcore.h
    src/kresult.c
    src/kdefer.c
    src/other.c
)

target_include_directories(libkcore PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
    $<INSTALL_INTERFACE:include>
)

set_target_properties(libkcore PROPERTIES
    VERSION 0.0.0
    PUBLIC_HEADER "src/kcore.h"
)

install(TARGETS libkcore
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
    PUBLIC_HEADER DESTINATION include
)
