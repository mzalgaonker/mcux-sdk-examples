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


project(snvs_lp_mc_cm7)

set(MCUX_SDK_PROJECT_NAME snvs_lp_mc_cm7.elf)

include(${ProjDirPath}/flags.cmake)

include(${ProjDirPath}/config.cmake)

add_executable(${MCUX_SDK_PROJECT_NAME} 
"${ProjDirPath}/../snvs_lp_mc.c"
"${ProjDirPath}/../pin_mux.c"
"${ProjDirPath}/../pin_mux.h"
"${ProjDirPath}/../../../../../../../core/boards/evkmimxrt1170/board.c"
"${ProjDirPath}/../../../../../../../core/boards/evkmimxrt1170/board.h"
"${ProjDirPath}/../../../../../../../core/boards/evkmimxrt1170/clock_config.c"
"${ProjDirPath}/../../../../../../../core/boards/evkmimxrt1170/clock_config.h"
"${ProjDirPath}/../../../../../../../core/boards/evkmimxrt1170/dcd.c"
"${ProjDirPath}/../../../../../../../core/boards/evkmimxrt1170/dcd.h"
"${ProjDirPath}/../evkmimxrt1170_connect_cm4_cm7side.jlinkscript"
)

target_include_directories(${MCUX_SDK_PROJECT_NAME} PRIVATE
    ${ProjDirPath}/..
    ${ProjDirPath}/../../../../../../../examples/evkmimxrt1170/driver_examples/snvs/snvs_lp_mc/cm7
    ${ProjDirPath}/../../../../../../../core/boards/evkmimxrt1170
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

include(driver_snvs_hp)

include(driver_snvs_lp)

include(driver_clock)

include(driver_common)

include(device_CMSIS)

include(component_lpuart_adapter)

include(component_lists)

include(driver_lpuart)

include(device_startup_MIMXRT1176_cm7)

include(driver_iomuxc)

include(driver_igpio)

include(driver_xip_device)

include(driver_xip_board_evkmimxrt1170)

include(driver_pmu_1)

include(driver_dcdc_soc)

include(driver_cache_armv7_m7)

include(driver_anatop_ai)

include(CMSIS_Include_core_cm)

include(utilities_misc_utilities)

include(device_system_MIMXRT1176_cm7)


TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--start-group)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE m)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE c)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE gcc)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE nosys)

TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--end-group)


