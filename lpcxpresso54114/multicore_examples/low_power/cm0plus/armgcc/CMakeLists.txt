# CROSS COMPILER SETTING
SET(CMAKE_SYSTEM_NAME Generic)
CMAKE_MINIMUM_REQUIRED (VERSION 3.1.1)

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


project(low_power_cm0plus)

set(MCUX_SDK_PROJECT_NAME low_power_cm0plus.elf)

include(${ProjDirPath}/flags.cmake)

include(${ProjDirPath}/config.cmake)

add_executable(${MCUX_SDK_PROJECT_NAME} 
"${ProjDirPath}/../low_power_core1.c"
"${ProjDirPath}/../static_queue.c"
"${ProjDirPath}/../static_queue.h"
"${ProjDirPath}/../low_power.h"
"${ProjDirPath}/../../sensors/bma2x2.c"
"${ProjDirPath}/../../sensors/bma2x2.h"
"${ProjDirPath}/../../sensors/bmi160.c"
"${ProjDirPath}/../../sensors/bmi160.h"
"${ProjDirPath}/../../sensors/bmm050.c"
"${ProjDirPath}/../../sensors/bmm050.h"
"${ProjDirPath}/../../sensors/bmp280.c"
"${ProjDirPath}/../../sensors/bmp280.h"
"${ProjDirPath}/../pin_mux.c"
"${ProjDirPath}/../pin_mux.h"
"${ProjDirPath}/../../../../../../core/boards/lpcxpresso54114/board.c"
"${ProjDirPath}/../../../../../../core/boards/lpcxpresso54114/board.h"
"${ProjDirPath}/../../../../../../core/boards/lpcxpresso54114/clock_config.c"
"${ProjDirPath}/../../../../../../core/boards/lpcxpresso54114/clock_config.h"
)

target_include_directories(${MCUX_SDK_PROJECT_NAME} PRIVATE
    ${ProjDirPath}/..
    ${ProjDirPath}/../../sensors
    ${ProjDirPath}/../../../../../../examples/lpcxpresso54114/multicore_examples/low_power/cm0plus
    ${ProjDirPath}/../../../../../../core/boards/lpcxpresso54114
)

#path for entry cmake
set(CMAKE_MODULE_PATH
    ${ProjDirPath}/../../../../../../core
)

#Include Entry cmake component
include(all_devices)

# include modules
include(driver_flexcomm_i2c)

include(utility_debug_console_lite)

include(utility_assert_lite)

include(driver_mailbox)

include(driver_utick)

include(driver_lpc_iocon)

include(driver_common)

include(driver_clock)

include(driver_power)

include(driver_reset)

include(device_CMSIS)

include(CMSIS_Include_core_cm0plus)

include(device_startup_LPC54114_cm0plus)

include(driver_flexcomm_usart)

include(driver_flexcomm)

include(driver_lpc_gpio)

include(component_usart_adapter)

include(component_lists)

include(utilities_misc_utilities)

include(CMSIS_Include_common)

include(CMSIS_Include_dsp)

include(device_system_LPC54114_cm0plus)


TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--start-group)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE m)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE c)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE gcc)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE nosys)

if(CMAKE_BUILD_TYPE STREQUAL debug)
    target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE ${ProjDirPath}/../../../../../../core/devices/LPC54114/gcc/libpower_cm0.a)
endif()

if(CMAKE_BUILD_TYPE STREQUAL release)
    target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE ${ProjDirPath}/../../../../../../core/devices/LPC54114/gcc/libpower_cm0.a)
endif()

TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--end-group)

ADD_CUSTOM_COMMAND(TARGET ${MCUX_SDK_PROJECT_NAME} POST_BUILD COMMAND ${CMAKE_OBJCOPY}
-Obinary ${EXECUTABLE_OUTPUT_PATH}/${MCUX_SDK_PROJECT_NAME} ${EXECUTABLE_OUTPUT_PATH}/core1_image.bin)

