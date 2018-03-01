include(${PROJECT_SOURCE_DIR}/cmake/CheckHeader.txt)
include(${PROJECT_SOURCE_DIR}/cmake/CheckSize.txt)
include(${PROJECT_SOURCE_DIR}/cmake/CheckSymbol.txt)
include(${PROJECT_SOURCE_DIR}/cmake/Flags.txt)

set(FUSE_DIR "${PROJECT_SOURCE_DIR}/cmake")

find_package(CURL REQUIRED)
find_package(FUSE REQUIRED)

configure_file(${PROJECT_SOURCE_DIR}/src/config.h.in ${PROJECT_BINARY_DIR}/inc/config.h)

set(src
    main.c)

list(SORT src)

include_directories("${PROJECT_BINARY_DIR}/inc")
include_directories("${CURL_INCLUDE_DIRS}")

set_source_files_properties(${src} PROPERTIES COMPILE_DEFINITIONS "${C_DEFINE}")

add_executable(fexfs ${src})
target_compile_options(fexfs PUBLIC ${C_FLAGS})
target_link_libraries(fexfs ${CMAKE_THREAD_LIBS_INIT} ${CURL_LIBRARIES} ${FUSE_LIBRARIES})

set(BINDIR bin)

install(TARGETS fexfs
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        RUNTIME DESTINATION bin)
