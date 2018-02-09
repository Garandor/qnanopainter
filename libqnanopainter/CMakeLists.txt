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
	"private/qnanobrush.h"
	"private/qnanodataelement.h"
	"private/qnanobackend.h"
	"private/qnanobackendfactory.h"
	"nanovg/nanovg.h"
        )

	    list(APPEND QNANOPAINTER_SRC 
	    "private/qnanobackendgles2.cpp"
	    "private/qnanobackendgles3.cpp"
	    )
	    list(APPEND QNANOPAINTER_HDR
	    "private/qnanobackendgles2.h"
	    "private/qnanobackendgles3.h"
		    )
	    list(APPEND QNANOPAINTER_SRC 
	    "private/qnanobackendgl2.cpp"
	    "private/qnanobackendgl3.cpp"
	    )
	    list(APPEND QNANOPAINTER_HDR
	    "private/qnanobackendgl2.h"
	    "private/qnanobackendgl3.h"
		    )


add_library(qnanopainter
	${QNANOPAINTER_SRC}
	${QNANOPAINTER_HDR}
	)

    #Windows does not provide OpenGL 2 or 3
    #Since Qt is assumed to be built -dynamic,
    #i.e. does not link to either OpenGL or GLES,
    #We need to do that manually 
    if(WIN32)
	    find_library(glesd NAMES libglesv2d  
		    HINTS $ENV{QT_DIR}/lib
		    )
	    find_library(gles NAMES libglesv2 
		    HINTS $ENV{QT_DIR}/lib
		    )
	    target_link_libraries(qnanopainter
	            debug ${glesd}
	            optimized ${gles}
	  	    )
    else()
        find_package(OpenGL)
        target_link_libraries(qnanopainter
            OpenGL::GL
            )
    endif()

target_link_libraries(qnanopainter
        Qt5::Quick
        Qt5::Gui
        )

target_include_directories(qnanopainter PRIVATE
        ${Qt5Quick_INCLUDE_DIRS}
        ${Qt5Gui_INCLUDE_DIRS}
        )
