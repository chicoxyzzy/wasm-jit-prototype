set(Sources ThreadTest.cpp)
set(PublicHeaders ${WAVM_INCLUDE_DIR}/ThreadTest/ThreadTest.h)
include_directories(${WAVM_INCLUDE_DIR}/ThreadTest)

WAVM_ADD_LIBRARY(ThreadTest ${Sources} ${PublicHeaders})

add_definitions(-DTHREADTEST_API=DLL_EXPORT)

target_link_libraries(ThreadTest Logging Platform Runtime)
