macro(print_all_variables)
    message(STATUS "print_all_variables------------------------------------------{")
    get_cmake_property(_variableNames VARIABLES)
    foreach (_variableName ${_variableNames})
        message(STATUS "${_variableName}=${${_variableName}}")
    endforeach()
    message(STATUS "print_all_variables------------------------------------------}")
endmacro()

macro(add_benchmark)
        set(singleValue NAME)
        set(multipleValues SOURCES)
        cmake_parse_arguments(local "" "${singleValue}" "${multipleValues}" ${ARGN})

        add_executable(${local_NAME} ${local_SOURCES})
        target_link_libraries(${local_NAME} boost_program_options poplar poputil popops poprand)
endmacro()

add_benchmark(
        NAME vertex_ipu_cont
        SOURCES vertex_ipu_cont.cpp)

add_benchmark(
        NAME vertex_ipu_nag
        SOURCES vertex_ipu_nag.cpp)

add_benchmark(
        NAME vertex_ipu_corner
        SOURCES vertex_ipu_corner.cpp)

add_benchmark(
        NAME vertex_ipu_prod
        SOURCES vertex_ipu_prod.cpp)

