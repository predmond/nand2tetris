macro(make_tests)
    get_filename_component(project_number "${CMAKE_CURRENT_SOURCE_DIR}" NAME)
    file(GLOB chips *.hdl)
    foreach(chip ${chips})
        get_filename_component(chip_name "${chip}" NAME_WE)
        add_test(NAME ${project_number}_${chip_name}_test
                 COMMAND ${CMAKE_SOURCE_DIR}/tools/HardwareSimulator.sh
                         ${CMAKE_CURRENT_SOURCE_DIR}/${chip_name}.tst)
        set_tests_properties(${project_number}_${chip_name}_test
                             PROPERTIES FAIL_REGULAR_EXPRESSION "Comparison failure")
    endforeach()
endmacro()

add_subdirectory(01)
add_subdirectory(02)
