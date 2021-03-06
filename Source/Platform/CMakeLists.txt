set(POSIXSources
	POSIX.cpp
	POSIX.S)

set(WindowsSources
	Windows.cpp
	Windows.asm)

set(PublicHeaders
	${WAVM_INCLUDE_DIR}/Platform/Platform.h)
include_directories(${WAVM_INCLUDE_DIR}/Platform)

if(CMAKE_SYSTEM_NAME STREQUAL "Darwin")
	include_directories(${CMAKE_PROJECT_DIR}/Source/ThirdParty/libunwind/include)
endif()

if(MSVC)
	set(Sources ${POSIXSources} ${WindowsSources})
	enable_language(ASM_MASM)
else()
	set(Sources ${POSIXSources})
endif()

add_definitions(-DPLATFORM_API=DLL_EXPORT)

WAVM_ADD_LIBRARY(Platform ${Sources} ${PublicHeaders})

if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
	# Link with dl on Linux for dladdr.
	target_link_libraries(Platform dl pthread rt)
endif()
