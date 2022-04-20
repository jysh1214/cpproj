set(SOURCES1 app1.cpp)
set(HEADERS1 )

set(SOURCES2 app2.cpp)
set(HEADERS2 )

set(INCS ${PROJECT_SOURCE_DIR}/lib)

set(LIBS MyLib1 MyLib2)

source_group("App1" FILES ${SOURCES1} ${HEADERS1})
source_group("App2" FILES ${SOURCES2} ${HEADERS2})

include_directories(${INCS})

add_executable(App1 ${SOURCES1})
target_link_libraries(App1 ${LIBS})

add_executable(App2 ${SOURCES2})
target_link_libraries(App2 ${LIBS})