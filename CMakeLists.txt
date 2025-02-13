set(COMPONENT_REQUIRES)
set(COMPONENT_PRIV_REQUIRES audio_sal audio_hal esp_dispatcher esp_peripherals display_service usb_device_uac)

if(CONFIG_AUDIO_BOARD_CUSTOM)
message(STATUS "Current board name is ESP32-S3-Box-3")
list(APPEND COMPONENT_ADD_INCLUDEDIRS ./esp32_s3_box_3)
set(COMPONENT_SRCS
./esp32_s3_box_3/board.c
./esp32_s3_box_3/board_pins_config.c
)
endif()

register_component()

idf_component_get_property(audio_board_lib audio_board COMPONENT_LIB)
set_property(TARGET ${audio_board_lib} APPEND PROPERTY INTERFACE_LINK_LIBRARIES ${COMPONENT_LIB})

# Add the directory containing the usb_device_uac component
list(APPEND EXTRA_COMPONENT_DIRS ${CMAKE_SOURCE_DIR}/components/usb_device_uac)
