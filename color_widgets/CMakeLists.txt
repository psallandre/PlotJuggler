

include_directories( ./include )

SET( CW_SRC
    include/color_names.hpp
    include/color_palette.hpp
    include/color_utils.hpp
    include/color_preview.hpp
    include/color_wheel.hpp
    include/swatch.hpp

    src/color_names.cpp
    src/color_palette.cpp
    src/color_utils.cpp
    src/color_preview.cpp
    src/color_wheel.cpp
    src/swatch.cpp
    )

add_library(colorwidgets ${CW_SRC})

target_link_libraries(colorwidgets
    ${Qt5Widgets_LIBRARIES} )
