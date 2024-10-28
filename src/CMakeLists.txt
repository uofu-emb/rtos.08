# This is the main binary. List your C files here.
add_executable(lab8
    main.c
    )

pico_set_program_name(lab8 "test")
pico_set_program_version(lab8 "0.1")

# Modify the below lines to enable/disable output over UART/USB.
# These are mutually exclusive, only set one.
pico_enable_stdio_uart(lab8 0)
pico_enable_stdio_usb(lab8 1)

# Add the libraries to the build
target_link_libraries(lab8 PRIVATE
  pico_stdlib
  pico_multicore
  pico_async_context_freertos
  can2040
  FreeRTOS-Kernel-Heap4
)

# Another pico macro which generates the uf2 file in addition to the elf
pico_add_extra_outputs(lab8)

add_custom_target(flash picotool load -f $<TARGET_FILE:lab8> DEPENDS lab8)
