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

target_link_libraries(qwt
    PUBLIC
    Qt${QT_VERSION}::Widgets
    Qt${QT_VERSION}::OpenGL
    Qt${QT_VERSION}::Svg
    Qt${QT_VERSION}::PrintSupport
    Qt${QT_VERSION}::Xml
    Qt${QT_VERSION}::Concurrent
)