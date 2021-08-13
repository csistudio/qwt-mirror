file(GLOB CPP_SOURCES *.cpp)
file(GLOB QRC_SOURCES *.qrc)
file(GLOB UI_SOURCES *.ui)

add_library( qwt STATIC
  ${CPP_SOURCES}
  ${QRC_SOURCES}
  ${UI_SOURCES}
)
target_include_directories(qwt PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_link_libraries(qwt PUBLIC Qt5::Widgets Qt5::OpenGL Qt5::Svg Qt5::PrintSupport Qt5::Xml Qt5::Concurrent)

target_compile_features(qwt PUBLIC ${STUDIO_CXX_STD})

target_compile_definitions(qwt PRIVATE QWT_MOC_INCLUDE=1)