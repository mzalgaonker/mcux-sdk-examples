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


project(dpu_character)

set(MCUX_SDK_PROJECT_NAME dpu_character.elf)

include(${ProjDirPath}/flags.cmake)

include(${ProjDirPath}/config.cmake)

add_executable(${MCUX_SDK_PROJECT_NAME} 
"${ProjDirPath}/../dpu_character.c"
"${ProjDirPath}/../pin_mux.c"
"${ProjDirPath}/../pin_mux.h"
"${ProjDirPath}/../dpu_board.c"
"${ProjDirPath}/../display_interface.c"
"${ProjDirPath}/../dpu_example.h"
"${ProjDirPath}/../../../../../../core/boards/mekmimx8qx/board.c"
"${ProjDirPath}/../../../../../../core/boards/mekmimx8qx/board.h"
"${ProjDirPath}/../../../../../../core/boards/mekmimx8qx/clock_config.c"
"${ProjDirPath}/../../../../../../core/boards/mekmimx8qx/clock_config.h"
"${ProjDirPath}/../empty_rsc_table.c"
)

target_include_directories(${MCUX_SDK_PROJECT_NAME} PRIVATE
    ${ProjDirPath}/..
    ${ProjDirPath}/../../../../../../examples/mekmimx8qx/driver_examples/dpu/character
    ${ProjDirPath}/../../../../../../core/boards/mekmimx8qx
)

#path for entry cmake
set(CMAKE_MODULE_PATH
    ${ProjDirPath}/../../../../../../core
)

#Include Entry cmake component
include(all_devices)

# include modules
include(driver_irqsteer)

include(driver_mipi_dsi)

include(driver_lpi2c)

include(driver_video-common)

include(driver_video-i2c)

include(driver_display-common)

include(driver_display-adv7535)

include(driver_display-rm67191)

include(driver_display-mipi-dsi-cmd)

include(driver_dpu_irqsteer)

include(driver_display-it6263)

include(driver_ldb_combo_phy)

include(driver_prg)

include(driver_dpr)

include(utility_debug_console_lite)

include(utility_assert_lite)

include(driver_clock)

include(driver_dpu)

include(driver_common)

include(device_CMSIS)

include(component_lpuart_adapter)

include(component_lists)

include(driver_lpuart)

include(device_startup)

include(driver_scfw_api)

include(driver_igpio)

include(CMSIS_Include_core_cm4)

include(CMSIS_Include_common)

include(CMSIS_Include_dsp)

include(utilities_misc_utilities)

include(device_system)


TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--start-group)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE m)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE c)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE gcc)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE nosys)

TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--end-group)

ADD_CUSTOM_COMMAND(TARGET ${MCUX_SDK_PROJECT_NAME} POST_BUILD COMMAND ${CMAKE_OBJCOPY}
-Obinary ${EXECUTABLE_OUTPUT_PATH}/${MCUX_SDK_PROJECT_NAME} ${EXECUTABLE_OUTPUT_PATH}/dpu_character.bin)

