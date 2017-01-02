macro(make_tests)
    file(RELATIVE_PATH prefix "${CMAKE_SOURCE_DIR}/projects" "${CMAKE_CURRENT_SOURCE_DIR}")
    string(REPLACE "/" "_" prefix ${prefix})
    file(GLOB chips *.tst)
    foreach(chip ${chips})
        get_filename_component(chip_name "${chip}" NAME_WE)
        add_test(NAME ${prefix}_${chip_name}_test
                 COMMAND ${CMAKE_SOURCE_DIR}/tools/HardwareSimulator.sh
                         ${CMAKE_CURRENT_SOURCE_DIR}/${chip_name}.tst)
        set_tests_properties(${prefix}_${chip_name}_test
                             PROPERTIES FAIL_REGULAR_EXPRESSION "Comparison failure")
    endforeach()
endmacro()

add_subdirectory(01)
add_subdirectory(02)
add_subdirectory(03)
