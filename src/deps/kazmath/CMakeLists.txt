project(kazmath)

include_directories(.)
if (IOS OR EMSCRIPTEN OR APPLE OR MSVC)
    include_directories(../lua/src)
else()
    include_directories(../luajit/src)
endif()

file(GLOB_RECURSE SOURCES *.c)
#file(GLOB_RECURSE REMOVE_SOURCES  
#  "jmemdos.c"
#  "jmemmac.c"
#)
#list(REMOVE_ITEM SOURCES ${REMOVE_SOURCES})
#message(${SOURCES})
file(GLOB_RECURSE HEADERS *.h)


add_library(kazmath OBJECT ${HEADERS} ${SOURCES})

if (IOS)
    set_target_properties(
            kazmath
            PROPERTIES
            XCODE_ATTRIBUTE_IPHONEOS_DEPLOYMENT_TARGET 9.0
    )
endif(IOS)
