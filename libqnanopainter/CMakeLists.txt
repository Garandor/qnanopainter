cmake_minimum_required(VERSION 3.1)

#QNanoPainter
# Find includes in corresponding build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)
# Instruct CMake to run moc automatically when needed.
set(CMAKE_AUTOMOC ON)

# Using QNANO_USE_RENDERNODE allows to pick up the bounding box on the go and just apply a transformation to normaliye the curve,
# otherwise, rendering on a FBO, the curve would be clipped

#headers are necessary for automoc to pick them up
set(QNANOPAINTER_SRC
        "qnanoquickitem.cpp"
        "qnanoquickitempainter.cpp"
        "qnanopainter.cpp"
        "qnanocolor.cpp"
        "qnanolineargradient.cpp"
        "qnanoimagepattern.cpp"
        "qnanoimage.cpp"
        "qnanofont.cpp"
        "qnanoradialgradient.cpp"
        "qnanoboxgradient.cpp"
        "private/qnanobackendgles2.cpp"
        "private/qnanobackendgles3.cpp"
        "private/qnanobackendgl2.cpp"
        "private/qnanobackendgl3.cpp"
        "nanovg/nanovg.c"
        )


set(QNANOPAINTER_HDR
        "qnanoboxgradient.h"
        "qnanocolor.h"
        "qnanofont.h"
        "qnanoimage.h"
        "qnanoimagepattern.h"
        "qnanolineargradient.h"
        "qnanopainter.h"
        "qnanoquickitem.h"
        "qnanoquickitempainter.h"
        "qnanoradialgradient.h"
        )

add_library(qnanopainter
	${QNANOPAINTER_SRC}
	${QNANOPAINTER_HDR}
	)

target_link_libraries(qnanopainter
	OpenGL::GL
        Qt5::Gui
        Qt5::Quick
        )

target_include_directories(qnanopainter PRIVATE
        ${OPENGL_INCLUDE_DIR}
        )
