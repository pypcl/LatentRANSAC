set(MODULE_NAME RunSingleTest)
project(${MODULE_NAME})

## Source files -----------------------------------------------------------------------------------

file(GLOB_RECURSE sources     "*.cpp")
file(GLOB_RECURSE headers_hpp "*.hpp")
file(GLOB_RECURSE headers_h   "*.h")
list(APPEND headers ${headers_h} ${headers_hpp})


## Project setup ----------------------------------------------------------------------------------

include_directories(
	${CONFIG++_INCLUDE_DIR}
	${USAC_SOURCE_DIR}
)

link_directories(
	${LAPACK_LIBRARY_DIRS}
)

add_executable(${MODULE_NAME}
	${sources}
	${headers}
)

target_link_libraries(${MODULE_NAME}
	${CONFIG++_LIBRARY}
	USAC
)

if(MSVC)
	add_definitions(/D_CRT_SECURE_NO_WARNINGS /MP)
endif(MSVC)
