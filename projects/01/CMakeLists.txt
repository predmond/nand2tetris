file(GLOB chips *.hdl)
foreach(chip ${chips})
	get_filename_component(chip_name "${chip}" NAME_WE)

	configure_file(${chip_name}.hdl ${chip_name}.hdl COPYONLY)
	configure_file(${chip_name}.tst ${chip_name}.tst COPYONLY)
	configure_file(${chip_name}.cmp ${chip_name}.cmp COPYONLY)

	add_test(NAME ${chip_name}_test COMMAND ${CMAKE_SOURCE_DIR}/tools/HardwareSimulator.sh ${chip_name}.tst)
	set_tests_properties(${chip_name}_test PROPERTIES FAIL_REGULAR_EXPRESSION "Comparison failure")
endforeach()
