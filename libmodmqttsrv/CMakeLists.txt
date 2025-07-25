set(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib")
set(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)

add_library(modmqttsrv
    STATIC
    config.cpp
    config.hpp
    conv_name_parser.cpp
    conv_name_parser.hpp
    debugtools.cpp
    debugtools.hpp
    default_command_converter.cpp
    default_command_converter.hpp
    logging.cpp
    logging.hpp
    modbus_client.cpp
    modbus_client.hpp
    modbus_context.cpp
    modbus_context.hpp
    modbus_executor.cpp
    modbus_executor.hpp
    modbus_messages.cpp
    modbus_messages.hpp
    modbus_request_queues.cpp
    modbus_request_queues.hpp
    modbus_scheduler.cpp
    modbus_scheduler.hpp
    modbus_slave.cpp
    modbus_slave.hpp
    modbus_thread.cpp
    modbus_thread.hpp
    modbus_types.cpp
    modbus_types.hpp
    modbus_watchdog.cpp
    modbus_watchdog.hpp
    modmqtt.cpp
    modmqtt.hpp
    mosquitto.cpp
    mosquitto.hpp
    mqttclient.cpp
    mqttclient.hpp
    mqttobject.cpp
    mqttobject.hpp
    mqttcommand.hpp
    mqttpayload.hpp
    mqttpayload.cpp
    queue_item.hpp
    register_poll.cpp
    register_poll.hpp
    yaml_converters.hpp
)

target_include_directories (modmqttsrv PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
set_target_properties(modmqttsrv PROPERTIES VERSION ${PROJECT_VERSION})
set_target_properties(modmqttsrv PROPERTIES SOVERSION 1)

if(DEFINED CMAKE_TOOLCHAIN_FILE AND CMAKE_TOOLCHAIN_FILE MATCHES "conan_toolchain.cmake")
    target_link_libraries(modmqttsrv
        PRIVATE
            mosquitto::mosquitto
            libmodbus::libmodbus
            yaml-cpp::yaml-cpp
            rapidjson
    )
endif()
