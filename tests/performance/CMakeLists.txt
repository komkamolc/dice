include_directories (
    .
    ${DICE_HEADER_DIRS}
    ${DICE_TRILINOS_HEADERS}
)


# glob all the cpp files
FILE ( GLOB test_cpp_files "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp")
FOREACH ( test_file ${test_cpp_files})
    # get the name of the test from the cpp filename
    GET_FILENAME_COMPONENT ( name ${test_file} NAME_WE)
    add_executable(${name} ${test_file})
    target_link_libraries(${name} ${DICE_LIBRARIES} dicecore)
    IF(DICE_ENABLE_NETCDF)
      target_link_libraries(${name} diceioutils ${NetCDF_lib})
    ENDIF()
ENDFOREACH ( )

