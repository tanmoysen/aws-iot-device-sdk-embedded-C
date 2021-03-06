set( DEMO_NAME "http_demo_basic_tls" )

# Include HTTP library's source and header path variables.
include( ${CMAKE_SOURCE_DIR}/libraries/standard/coreHTTP/httpFilePaths.cmake )

# Demo target.
add_executable(${DEMO_NAME})

target_sources(
    ${DEMO_NAME}
    PRIVATE
        "${DEMO_NAME}.c"
        ${HTTP_SOURCES}
        ${HTTP_THIRD_PARTY_SOURCES}
)

target_link_libraries(
    ${DEMO_NAME}
    PRIVATE
        openssl_posix
)

target_include_directories(
    ${DEMO_NAME}
    PUBLIC
        ${HTTP_INCLUDE_PUBLIC_DIRS}
        ${HTTP_INCLUDE_THIRD_PARTY_DIRS}
        ${HTTP_INCLUDE_PRIVATE_DIRS}
        ${CMAKE_CURRENT_LIST_DIR}
        ${LOGGING_INCLUDE_DIRS}
)

if(ROOT_CA_CERT_PATH)
    target_compile_definitions(
        ${DEMO_NAME} PRIVATE
            ROOT_CA_CERT_PATH="${ROOT_CA_CERT_PATH}"
    )
endif()
if(SERVER_HOST)
    target_compile_definitions(
        ${DEMO_NAME} PRIVATE
            SERVER_HOST="${SERVER_HOST}"
    )
endif()
