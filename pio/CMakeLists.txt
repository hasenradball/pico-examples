if (TARGET hardware_pio)
    add_subdirectory_exclude_platforms(addition)
    add_subdirectory_exclude_platforms(apa102)
    add_subdirectory_exclude_platforms(clocked_input)
    add_subdirectory_exclude_platforms(differential_manchester)
    add_subdirectory_exclude_platforms(hello_pio)
    add_subdirectory_exclude_platforms(hub75)
    add_subdirectory_exclude_platforms(i2c)
    add_subdirectory_exclude_platforms(ir_nec)
    add_subdirectory_exclude_platforms(logic_analyser)
    add_subdirectory_exclude_platforms(manchester_encoding)
    add_subdirectory_exclude_platforms(onewire)
    add_subdirectory_exclude_platforms(pio_blink)
    add_subdirectory_exclude_platforms(pwm)
    add_subdirectory_exclude_platforms(quadrature_encoder)
    add_subdirectory_exclude_platforms(quadrature_encoder_substep)
    add_subdirectory_exclude_platforms(spi)
    add_subdirectory_exclude_platforms(squarewave)
    add_subdirectory_exclude_platforms(st7789_lcd)
    add_subdirectory_exclude_platforms(uart_dma)
    add_subdirectory_exclude_platforms(uart_rx)
    add_subdirectory_exclude_platforms(uart_tx)
    add_subdirectory_exclude_platforms(ws2812)
else()
    message("Skipping PIO examples as hardware_pio is unavailable on this platform")
endif()
