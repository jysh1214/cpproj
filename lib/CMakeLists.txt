set(SOURCES1 my_func1.cpp)
set(HEADERS1 my_func1.h)

set(SOURCES2 my_func2.cpp)
set(HEADERS2 my_func2.h)

set(LIBS )

source_group("MyFunc1" FILES ${SOURCES1} ${HEADERS1})
source_group("MyFunc2" FILES ${SOURCES2} ${HEADERS2})

add_library(MyLib1 ${SOURCES1} ${HEADERS1})
target_link_libraries(MyLib1 ${LIBS})

add_library(MyLib2 ${SOURCES2} ${HEADERS2})
target_link_libraries(MyLib2 ${LIBS})