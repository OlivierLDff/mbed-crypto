add_executable(${MBEDCRYPTO_EXAMPLES_PREFIX_}crypto_examples crypto_examples.c)
target_link_libraries(${MBEDCRYPTO_EXAMPLES_PREFIX_}crypto_examples ${MBEDCRYPTO_TARGET})
SET_TARGET_PROPERTIES(${MBEDCRYPTO_EXAMPLES_PREFIX_}crypto_examples PROPERTIES FOLDER ${MBEDCRYPTO_FOLDER_PREFIX}/Examples/psa)

add_executable(${MBEDCRYPTO_EXAMPLES_PREFIX_}key_ladder_demo key_ladder_demo.c)
target_link_libraries(${MBEDCRYPTO_EXAMPLES_PREFIX_}key_ladder_demo ${MBEDCRYPTO_TARGET})
SET_TARGET_PROPERTIES(${MBEDCRYPTO_EXAMPLES_PREFIX_}key_ladder_demo PROPERTIES FOLDER ${MBEDCRYPTO_FOLDER_PREFIX}/Examples/psa)

add_executable(${MBEDCRYPTO_EXAMPLES_PREFIX_}psa_constant_names psa_constant_names.c)
target_link_libraries(${MBEDCRYPTO_EXAMPLES_PREFIX_}psa_constant_names ${MBEDCRYPTO_TARGET})
SET_TARGET_PROPERTIES(${MBEDCRYPTO_EXAMPLES_PREFIX_}psa_constant_names PROPERTIES FOLDER ${MBEDCRYPTO_FOLDER_PREFIX}/Examples/psa)

add_custom_target(
    ${MBEDCRYPTO_EXAMPLES_PREFIX_}psa_constant_names_generated
    COMMAND ${PYTHON_EXECUTABLE} scripts/generate_psa_constants.py
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/../../
)
SET_TARGET_PROPERTIES(${MBEDCRYPTO_EXAMPLES_PREFIX_}psa_constant_names_generated PROPERTIES FOLDER ${MBEDCRYPTO_FOLDER_PREFIX}/Examples/psa/generated)
add_dependencies(${MBEDCRYPTO_EXAMPLES_PREFIX_}psa_constant_names ${MBEDCRYPTO_EXAMPLES_PREFIX_}psa_constant_names_generated)

IF(MBEDCRYPTO_ENABLE_INSTALL)
install(TARGETS
            ${MBEDCRYPTO_EXAMPLES_PREFIX_}crypto_examples
            ${MBEDCRYPTO_EXAMPLES_PREFIX_}key_ladder_demo
            ${MBEDCRYPTO_EXAMPLES_PREFIX_}psa_constant_names
        DESTINATION "bin"
        PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE)

install(PROGRAMS
            key_ladder_demo.sh
        DESTINATION "bin")
ENDIF(MBEDCRYPTO_ENABLE_INSTALL)