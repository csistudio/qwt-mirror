file(GLOB CPP_SOURCES *.cpp)
file(GLOB QRC_SOURCES *.qrc)
file(GLOB UI_SOURCES *.ui)

add_library(qwt STATIC
    ${CPP_SOURCES}
    ${QRC_SOURCES}
    ${UI_SOURCES}
)

target_include_directories(qwt PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_compile_features(qwt PUBLIC ${STUDIO_CXX_STD})
target_compile_definitions(qwt PRIVATE QWT_MOC_INCLUDE=1)

# --- Detect which Qt version is already available and link accordingly ---
if (TARGET Qt6::Widgets)
    message(STATUS "Linking qwt with Qt6 targets")
    target_link_libraries(qwt
        PUBLIC
            Qt6::Widgets
            Qt6::OpenGL
            Qt6::Svg
            Qt6::PrintSupport
            Qt6::Xml
            Qt6::Concurrent
    )

elseif (TARGET Qt5::Widgets)
    message(STATUS "Linking qwt with Qt5 targets")
    target_link_libraries(qwt
        PUBLIC
            Qt5::Widgets
            Qt5::OpenGL
            Qt5::Svg
            Qt5::PrintSupport
            Qt5::Xml
            Qt5::Concurrent
    )

else()
    message(FATAL_ERROR "Neither Qt5 nor Qt6 targets are available in this project!")
endif()