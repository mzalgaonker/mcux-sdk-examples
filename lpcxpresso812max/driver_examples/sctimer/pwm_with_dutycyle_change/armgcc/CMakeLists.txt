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


project(sctimer_pwm_with_dutycyle_change)

set(MCUX_SDK_PROJECT_NAME sctimer_pwm_with_dutycyle_change.elf)

include(${ProjDirPath}/flags.cmake)
include(${ProjDirPath}/config.cmake)

add_executable(${MCUX_SDK_PROJECT_NAME} 
"${ProjDirPath}/../sctimer_update_dutycycle.c"
"${ProjDirPath}/../pin_mux.c"
"${ProjDirPath}/../pin_mux.h"
"${ProjDirPath}/../../../../../../core/boards/lpcxpresso812max/board.c"
"${ProjDirPath}/../../../../../../core/boards/lpcxpresso812max/board.h"
"${ProjDirPath}/../../../../../../core/boards/lpcxpresso812max/clock_config.c"
"${ProjDirPath}/../../../../../../core/boards/lpcxpresso812max/clock_config.h"
)

target_include_directories(${MCUX_SDK_PROJECT_NAME} PRIVATE
    ${ProjDirPath}/..
    ${ProjDirPath}/../../../../../../examples/lpcxpresso812max/driver_examples/sctimer/pwm_with_dutycyle_change
    ${ProjDirPath}/../../../../../../core/boards/lpcxpresso812max
)

#path for entry cmake
set(CMAKE_MODULE_PATH
    ${ProjDirPath}/../../../../../../core
)

#Include Entry cmake component
include(all_devices)

# include modules
include(utility_debug_console_lite)

include(utility_assert_lite)

include(driver_sctimer)

include(driver_lpc_gpio)

include(driver_common)

include(driver_clock)

include(driver_power_no_lib)

include(driver_swm)

include(driver_syscon)

include(device_CMSIS)

include(component_miniusart_adapter)

include(device_startup)

include(driver_lpc_miniusart)

include(driver_lpc_iocon_lite)

include(CMSIS_Include_core_cm0plus)

include(CMSIS_Include_common)

include(CMSIS_Include_dsp)

include(driver_reset)

include(utilities_misc_utilities)

include(driver_swm_connections)

include(driver_syscon_connections)

include(device_system)


TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--start-group)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE m)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE c)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE gcc)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE nosys)

TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--end-group)


