PROJECT(sqlite3)
cmake_minimum_required(VERSION 2.8)

include_directories(${CMAKE_SOURCE_DIR}/src)
add_library(sqlite3 SHARED src/sqlite3.c src/sqlite3.h src/sqlite3ext.h)
add_executable(sqlite src/sqlite3.c src/shell.c src/sqlite3.h src/sqlite3ext.h)
target_link_libraries(sqlite m ${CMAKE_DL_LIBS})
set_target_properties(sqlite PROPERTIES OUTPUT_NAME sqlite3)

add_definitions(-DSQLITE_ENABLE_RTREE)
add_definitions(-DSQLITE_ENABLE_FTS4)
add_definitions(-DSQLITE_ENABLE_FTS5)
add_definitions(-DSQLITE_ENABLE_JSON1)
add_definitions(-DSQLITE_THREADSAFE=0)
add_definitions(-DSQLITE_ENABLE_COLUMN_METADATA)


install(FILES src/sqlite3.h src/sqlite3ext.h DESTINATION include)
install(TARGETS sqlite3 LIBRARY DESTINATION lib ARCHIVE DESTINATION lib)
install(TARGETS sqlite RUNTIME DESTINATION bin)

