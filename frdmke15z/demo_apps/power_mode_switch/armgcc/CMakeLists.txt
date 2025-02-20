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


project(power_mode_switch)

set(MCUX_SDK_PROJECT_NAME power_mode_switch.elf)

include(${ProjDirPath}/flags.cmake)

include(${ProjDirPath}/config.cmake)

add_executable(${MCUX_SDK_PROJECT_NAME} 
"${ProjDirPath}/../clock_scg.c"
"${ProjDirPath}/../peripherals.c"
"${ProjDirPath}/../peripherals.h"
"${ProjDirPath}/../power_mode_switch.c"
"${ProjDirPath}/../power_mode_switch.h"
"${ProjDirPath}/../pin_mux.c"
"${ProjDirPath}/../pin_mux.h"
"${ProjDirPath}/../../../../../core/boards/frdmke15z/board.c"
"${ProjDirPath}/../../../../../core/boards/frdmke15z/board.h"
"${ProjDirPath}/../../../../../core/boards/frdmke15z/clock_config.c"
"${ProjDirPath}/../../../../../core/boards/frdmke15z/clock_config.h"
)

target_include_directories(${MCUX_SDK_PROJECT_NAME} PRIVATE
    ${ProjDirPath}/../../../../../examples/frdmke15z/demo_apps/power_mode_switch
    ${ProjDirPath}/..
    ${ProjDirPath}/../../../../../core/boards/frdmke15z
)

#path for entry cmake
set(CMAKE_MODULE_PATH
    ${ProjDirPath}/../../../../../core
)

#Include Entry cmake component
include(all_devices)

# include modules
include(driver_port)

include(driver_pmc)

include(driver_smc)

include(driver_rcm)

include(driver_lptmr)

include(driver_gpio)

include(driver_clock)

include(driver_common)

include(device_CMSIS)

include(utility_debug_console)

include(component_lpuart_adapter)

include(component_serial_manager)

include(component_lists)

include(component_serial_manager_uart)

include(driver_lpuart)

include(device_startup)

include(utility_assert)

include(CMSIS_Include_core_cm)

include(utilities_misc_utilities)

include(device_system)


TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--start-group)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE m)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE c)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE gcc)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE nosys)

TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--end-group)


