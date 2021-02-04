if (BUILD_TESTING)
    file(COPY ${CMAKE_SOURCE_DIR}/tests/data DESTINATION ${CMAKE_BINARY_DIR}/tests)

    file(GLOB CATACLYSM_DDA_TEST_SOURCES
            ${CMAKE_SOURCE_DIR}/tests/*.cpp)

    # Enabling benchmarks
    add_definitions(-DCATCH_CONFIG_ENABLE_BENCHMARKING)

    if (TILES)
        add_executable(cata_test-tiles ${CATACLYSM_DDA_TEST_SOURCES})
        set_target_properties(cata_test-tiles PROPERTIES INTERPROCEDURAL_OPTIMIZATION ${LTO})
        target_link_libraries(cata_test-tiles cataclysm-tiles-common)
        add_test(NAME test-tiles
                COMMAND sh -c
                "$<TARGET_FILE:cata_test-tiles> -r cata --rng-seed `shuf -i 0-1000000000 -n 1`"
                WORKING_DIRECTORY ${CMAKE_SOURCE_DIR})
    endif ()

    if (CURSES)
        add_executable(cata_test ${CATACLYSM_DDA_TEST_SOURCES})
        set_target_properties(cata_test PROPERTIES INTERPROCEDURAL_OPTIMIZATION ${LTO})
        target_link_libraries(cata_test cataclysm-common)
        add_test(NAME test
                COMMAND sh -c
                "$<TARGET_FILE:cata_test> -r cata --rng-seed `shuf -i 0-1000000000 -n 1`"
                WORKING_DIRECTORY ${CMAKE_SOURCE_DIR})
    endif ()
endif ()
