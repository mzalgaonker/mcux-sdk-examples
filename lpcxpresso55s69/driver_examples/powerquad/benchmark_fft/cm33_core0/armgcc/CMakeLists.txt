# CROSS COMPILER SETTING
SET(CMAKE_SYSTEM_NAME Generic)
CMAKE_MINIMUM_REQUIRED (VERSION 3.10.0)

# THE VERSION NUMBER
SET (Tutorial_VERSION_MAJOR 1)
SET (Tutorial_VERSION_MINOR 0)

# ENABLE ASM
ENABLE_LANGUAGE(ASM)

SET(CMAKE_STATIC_LIBRARY_PREFIX)
SET(CMAKE_STATIC_LIBRARY_SUFFIX)

SET(CMAKE_EXECUTABLE_LIBRARY_PREFIX)
SET(CMAKE_EXECUTABLE_LIBRARY_SUFFIX)

# CURRENT DIRECTORY
SET(ProjDirPath ${CMAKE_CURRENT_SOURCE_DIR})

SET(EXECUTABLE_OUTPUT_PATH ${ProjDirPath}/${CMAKE_BUILD_TYPE})
SET(LIBRARY_OUTPUT_PATH ${ProjDirPath}/${CMAKE_BUILD_TYPE})


project(powerquad_benchmark_fft)

set(MCUX_SDK_PROJECT_NAME powerquad_benchmark_fft.elf)

include(${ProjDirPath}/flags.cmake)

include(${ProjDirPath}/config.cmake)

add_executable(${MCUX_SDK_PROJECT_NAME} 
"${ProjDirPath}/../powerquad_benchmark_fft.c"
"${ProjDirPath}/../pin_mux.c"
"${ProjDirPath}/../pin_mux.h"
"${ProjDirPath}/../../../../../../../core/boards/lpcxpresso55s69/board.c"
"${ProjDirPath}/../../../../../../../core/boards/lpcxpresso55s69/board.h"
"${ProjDirPath}/../../../../../../../core/boards/lpcxpresso55s69/clock_config.c"
"${ProjDirPath}/../../../../../../../core/boards/lpcxpresso55s69/clock_config.h"
)

target_include_directories(${MCUX_SDK_PROJECT_NAME} PRIVATE
    ${ProjDirPath}/..
    ${ProjDirPath}/../../../../../../../core/boards/lpcxpresso55s69
    ${ProjDirPath}/../../../../../../../examples/lpcxpresso55s69/driver_examples/powerquad/benchmark_fft
)

#path for entry cmake
set(CMAKE_MODULE_PATH
    ${ProjDirPath}/../../../../../../../core
)

#Include Entry cmake component
include(all_devices)

# include modules
include(utility_debug_console_lite)

include(utility_assert_lite)

include(driver_powerquad)

include(driver_common)

include(driver_power)

include(driver_lpc_iocon)

include(driver_lpc_gpio)

include(driver_inputmux)

include(driver_clock)

include(device_CMSIS)

include(device_startup_LPC55S69_cm33_core0)

include(driver_flexcomm_usart)

include(driver_flexcomm)

include(component_usart_adapter)

include(component_lists)

include(CMSIS_Include_core_cm)

include(driver_reset)

include(CMSIS_DSP_Library)

include(driver_inputmux_connections)

include(utilities_misc_utilities)

include(device_system_LPC55S69_cm33_core0)


TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--start-group)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE m)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE c)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE gcc)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE nosys)

if(CMAKE_BUILD_TYPE STREQUAL debug)
    target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE ${ProjDirPath}/../../../../../../../core/devices/LPC55S69/gcc/libpower_hardabi.a)
endif(CMAKE_BUILD_TYPE STREQUAL debug)

if(CMAKE_BUILD_TYPE STREQUAL debug)
    target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE ${ProjDirPath}/../../../../../../../core/CMSIS/DSP/Lib/GCC/libarm_ARMv8MMLldfsp_math.a)
endif(CMAKE_BUILD_TYPE STREQUAL debug)

if(CMAKE_BUILD_TYPE STREQUAL release)
    target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE ${ProjDirPath}/../../../../../../../core/devices/LPC55S69/gcc/libpower_hardabi.a)
endif(CMAKE_BUILD_TYPE STREQUAL release)

if(CMAKE_BUILD_TYPE STREQUAL release)
    target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE ${ProjDirPath}/../../../../../../../core/CMSIS/DSP/Lib/GCC/libarm_ARMv8MMLldfsp_math.a)
endif(CMAKE_BUILD_TYPE STREQUAL release)

TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--end-group)


