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


project(power_mode_switch_m40)

set(MCUX_SDK_PROJECT_NAME power_mode_switch_m40.elf)

include(${ProjDirPath}/flags.cmake)

include(${ProjDirPath}/config.cmake)

add_executable(${MCUX_SDK_PROJECT_NAME} 
"${ProjDirPath}/../rsc_table.c"
"${ProjDirPath}/../rsc_table.h"
"${ProjDirPath}/../remoteproc.h"
"${ProjDirPath}/../../../../../../core/boards/mekmimx8qm/board.c"
"${ProjDirPath}/../../../../../../core/boards/mekmimx8qm/board.h"
"${ProjDirPath}/../../../../../../core/boards/mekmimx8qm/clock_config.c"
"${ProjDirPath}/../../../../../../core/boards/mekmimx8qm/clock_config.h"
"${ProjDirPath}/../lpm.c"
"${ProjDirPath}/../lpm.h"
"${ProjDirPath}/../gcc/lpm_asm.S"
"${ProjDirPath}/../power_mode_switch.c"
"${ProjDirPath}/../power_mode_switch.h"
"${ProjDirPath}/../pin_mux.c"
"${ProjDirPath}/../pin_mux.h"
"${ProjDirPath}/../FreeRTOSConfig.h"
"${ProjDirPath}/../rpmsg_config.h"
)

target_include_directories(${MCUX_SDK_PROJECT_NAME} PRIVATE
    ${ProjDirPath}/.. debug
    ${ProjDirPath}/..
    ${ProjDirPath}/../../../../../../core/boards/mekmimx8qm
    ${ProjDirPath}/../../../../../../examples/mekmimx8qm/demo_apps/power_mode_switch/cm4_core0
)

#path for entry cmake
set(CMAKE_MODULE_PATH
    ${ProjDirPath}/../../../../../../core
)

#Include Entry cmake component
include(all_devices)

# include modules
include(middleware_multicore_rpmsg_lite_imx8qm_m4_freertos)

include(driver_asmc)

include(driver_irqsteer)

include(driver_gpt)

include(driver_tstmr)

include(driver_igpio)

include(driver_lpit)

include(driver_wdog32)

include(driver_sc_event)

include(driver_lpi2c)

include(driver_mu)

include(driver_memory)

include(driver_cache_lmem)

include(middleware_freertos-kernel_heap_4)

include(driver_clock)

include(driver_common)

include(device_CMSIS)

include(device_startup_MIMX8QM6_cm4_core0)

include(driver_lpuart)

include(driver_scfw_api)

include(utility_assert)

include(utility_debug_console)

include(component_lpuart_adapter)

include(component_serial_manager)

include(component_lists)

include(component_serial_manager_uart)

include(middleware_multicore_rpmsg_lite)

include(middleware_freertos-kernel_MIMX8QM6_cm4_core0)

include(middleware_freertos-kernel_extension)

include(CMSIS_Include_core_cm4)

include(CMSIS_Include_common)

include(CMSIS_Include_dsp)

include(utilities_misc_utilities)


TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--start-group)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE m)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE c)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE gcc)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE nosys)

TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--end-group)

ADD_CUSTOM_COMMAND(TARGET ${MCUX_SDK_PROJECT_NAME} POST_BUILD COMMAND ${CMAKE_OBJCOPY}
-Obinary ${EXECUTABLE_OUTPUT_PATH}/${MCUX_SDK_PROJECT_NAME} ${EXECUTABLE_OUTPUT_PATH}/power_mode_switch_m40.bin)

