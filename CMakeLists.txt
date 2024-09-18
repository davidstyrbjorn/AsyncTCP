idf_build_get_property(__hack_component_targets __COMPONENT_TARGETS)

if("arduino" IN_LIST BUILD_COMPONENTS OR __hack_component_targets MATCHES "__idf_arduino")
    message("arduino detected")
    list(APPEND ASYNC_TCP_PRIV_REQUIRES
        arduino
    )
elseif("framework-arduinoespressif32" IN_LIST BUILD_COMPONENTS OR __hack_component_targets MATCHES "___idf_framework-arduinoespressif32")
    message("arduinoespressif32 detected")
    list(APPEND ASYNC_TCP_PRIV_REQUIRES
        framework-arduinoespressif32
    )
elseif("espressif__arduino-esp32" IN_LIST BUILD_COMPONENTS OR __hack_component_targets MATCHES "___idf_espressif__arduino-esp32")
    message("arduino-esp32 detected")
    list(APPEND ASYNC_TCP_PRIV_REQUIRES
        espressif__arduino-esp32
    )
endif()

set(COMPONENT_SRCDIRS
    "src"
)

set(COMPONENT_ADD_INCLUDEDIRS
    "src"
)

idf_component_register(
    SRCS "src/AsyncTCP.cpp"
    INCLUDE_DIRS "src"
    PRIV_REQUIRES ${ASYNC_TCP_PRIV_REQUIRES}
)

target_compile_options(${COMPONENT_TARGET} PRIVATE -fno-rtti)
