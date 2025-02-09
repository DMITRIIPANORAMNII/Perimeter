INCLUDE_DIRECTORIES(
    BEFORE .
    "${PROJECT_SOURCE_DIR}/Source/XTool"
    "${PROJECT_SOURCE_DIR}/Source/Util"
)

SET(XPrm_SRCS
    StdAfx.cpp
    Token.cpp
)

SET(XPrm_LINK_LIBS ${EXE_LINK_LIBS_PRE} XTool ${SDL2_LIBRARY} ${EXE_LINK_LIBS_POST})

IF(PERIMETER_DEBUG)
    SET(XPrm_SRCS ${XPrm_SRCS} RunTimeCompiler.cpp)
ENDIF()
IF(PERIMETER_EXODUS)
    SET(XPrm_LINK_LIBS ${XPrm_LINK_LIBS} Exodus)
ENDIF()

ADD_EXECUTABLE(XPrm ${XPrm_SRCS} XPrm.cpp)
target_compile_options(XPrm PRIVATE ${PERIMETER_COMPILE_OPTIONS})
TARGET_LINK_LIBRARIES(XPrm PRIVATE ${XPrm_LINK_LIBS})

IF(PERIMETER_DEBUG)
    ADD_LIBRARY(XPrmLib STATIC ${XPrm_SRCS})
    target_compile_options(XPrmLib PRIVATE ${PERIMETER_COMPILE_OPTIONS})
    TARGET_LINK_LIBRARIES(XPrmLib PRIVATE ${XPrm_LINK_LIBS})
ENDIF()
