set(libs
    ${MBEDCRYPTO_TARGET}
)

add_executable(${MBEDCRYPTO_EXAMPLES_PREFIX_}selftest selftest.c)
target_link_libraries(${MBEDCRYPTO_EXAMPLES_PREFIX_}selftest ${libs})
SET_TARGET_PROPERTIES(${MBEDCRYPTO_EXAMPLES_PREFIX_}selftest PROPERTIES FOLDER ${MBEDCRYPTO_FOLDER_PREFIX}/Examples/test)

add_executable(${MBEDCRYPTO_EXAMPLES_PREFIX_}benchmark benchmark.c)
target_link_libraries(${MBEDCRYPTO_EXAMPLES_PREFIX_}benchmark ${libs})
SET_TARGET_PROPERTIES(${MBEDCRYPTO_EXAMPLES_PREFIX_}benchmark PROPERTIES FOLDER ${MBEDCRYPTO_FOLDER_PREFIX}/Examples/test)

if(TEST_CPP)
    add_executable(${MBEDCRYPTO_EXAMPLES_PREFIX_}cpp_dummy_build cpp_dummy_build.cpp)
    target_link_libraries(${MBEDCRYPTO_EXAMPLES_PREFIX_}cpp_dummy_build ${libs})
    SET_TARGET_PROPERTIES(${MBEDCRYPTO_EXAMPLES_PREFIX_}cpp_dummy_build PROPERTIES FOLDER ${MBEDCRYPTO_FOLDER_PREFIX}/Examples/test)
endif()


add_executable(${MBEDCRYPTO_EXAMPLES_PREFIX_}zeroize zeroize.c)
target_link_libraries(${MBEDCRYPTO_EXAMPLES_PREFIX_}zeroize ${libs})
SET_TARGET_PROPERTIES(${MBEDCRYPTO_EXAMPLES_PREFIX_}zeroize PROPERTIES FOLDER ${MBEDCRYPTO_FOLDER_PREFIX}/Examples/test)

add_executable(${MBEDCRYPTO_EXAMPLES_PREFIX_}query_compile_time_config query_compile_time_config.c)
target_sources(${MBEDCRYPTO_EXAMPLES_PREFIX_}query_compile_time_config PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/query_config.c)
target_link_libraries(${MBEDCRYPTO_EXAMPLES_PREFIX_}query_compile_time_config ${libs})
SET_TARGET_PROPERTIES(${MBEDCRYPTO_EXAMPLES_PREFIX_}query_compile_time_config PROPERTIES FOLDER ${MBEDCRYPTO_FOLDER_PREFIX}/Examples/test)

IF(MBEDCRYPTO_ENABLE_INSTALL)
install(TARGETS ${MBEDCRYPTO_EXAMPLES_PREFIX_}selftest ${MBEDCRYPTO_EXAMPLES_PREFIX_}benchmark ${MBEDCRYPTO_EXAMPLES_PREFIX_}query_compile_time_config
        DESTINATION "bin"
        PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE)
ENDIF(MBEDCRYPTO_ENABLE_INSTALL)