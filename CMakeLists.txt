# == DO NOT EDIT THE FOLLOWING LINES for the Raspberry Pi Pico VS Code Extension to work ==
if(WIN32)
    set(USERHOME $ENV{USERPROFILE})
else()
    set(USERHOME $ENV{HOME})
endif()
set(sdkVersion 2.1.0)
set(toolchainVersion 13_3_Rel1)
set(picotoolVersion 2.1.0)
set(picoVscode ${USERHOME}/.pico-sdk/cmake/pico-vscode.cmake)
if (EXISTS ${picoVscode})
    include(${picoVscode})
endif()
# ====================================================================================
set(PICO_BOARD pico CACHE STRING "Board type")

cmake_minimum_required(VERSION 3.13)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Inicializa o SDK do Raspberry Pi Pico
include(pico_sdk_import.cmake)

project(pioprojetofinal8 C CXX ASM)

# Inicializa o SDK do Pico
pico_sdk_init()

# Define o executável do projeto, especificando o arquivo principal (main.c)
add_executable(pioprojetofinal8 main.c)

# Gera o header PIO
pico_generate_pio_header(pioprojetofinal8 ${CMAKE_CURRENT_LIST_DIR}/ws2818b.pio)

pico_set_program_name(pioprojetofinal8 "pioprojetofinal8")
pico_set_program_version(pioprojetofinal8 "0.1")

# Habilita a saída padrão via USB (para depuração)
pico_enable_stdio_usb(pioprojetofinal8 1)
pico_enable_stdio_uart(pioprojetofinal8 0)

# Linka as bibliotecas necessárias: stdlib, hardware_adc, hardware_pwm e PIO
target_link_libraries(pioprojetofinal8
    pico_stdlib
    hardware_adc
    hardware_pwm
    hardware_pio
    hardware_clocks
)

# Adiciona os diretórios de inclusão
target_include_directories(pioprojetofinal8 PRIVATE ${CMAKE_CURRENT_LIST_DIR})

# Gera arquivos binários extras (UF2, HEX, ELF, etc.)
pico_add_extra_outputs(pioprojetofinal8)

# Define a URL de referência para este exemplo (opcional)
# Isso é útil se você estiver compartilhando o código e quiser apontar para uma fonte online
#example_auto_set_url(pioprojetofinal8)
