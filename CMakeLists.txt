cmake_minimum_required(VERSION 3.12)
project(LZ4 C)

# --- LZ4 Library (static) ---
add_library(lz4_static STATIC
    lib/lz4.c
    lib/lz4hc.c
    lib/lz4frame.c
    lib/xxhash.c     # REQUIRED for LZ4 Frame
)

target_include_directories(lz4_static PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/lib
)

# --- CLI Executable ---
add_executable(lz4sai
    programs/bench.c    
    programs/lz4cli.c     
    programs/threadpool.c   
    programs/util.c
    programs/lorem.c
    programs/lz4io.c
    programs/timefn.c
)
    

target_include_directories(lz4sai PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/lib
    ${CMAKE_CURRENT_SOURCE_DIR}/programs
)

target_link_libraries(lz4sai PRIVATE lz4_static)


install(TARGETS lz4sai
        RUNTIME DESTINATION bin)
