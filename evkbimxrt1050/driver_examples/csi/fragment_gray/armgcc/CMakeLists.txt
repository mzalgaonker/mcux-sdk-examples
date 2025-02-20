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


project(csi_fragment_gray)

set(MCUX_SDK_PROJECT_NAME csi_fragment_gray.elf)

include(${ProjDirPath}/flags.cmake)

include(${ProjDirPath}/config.cmake)

add_executable(${MCUX_SDK_PROJECT_NAME} 
"${ProjDirPath}/../csi_fragment_gray.c"
"${ProjDirPath}/../pin_mux.c"
"${ProjDirPath}/../pin_mux.h"
"${ProjDirPath}/../../../../../../core/boards/evkbimxrt1050/board.c"
"${ProjDirPath}/../../../../../../core/boards/evkbimxrt1050/board.h"
"${ProjDirPath}/../../../../../../core/boards/evkbimxrt1050/clock_config.c"
"${ProjDirPath}/../../../../../../core/boards/evkbimxrt1050/clock_config.h"
"${ProjDirPath}/../../../../../../core/boards/evkbimxrt1050/dcd.c"
"${ProjDirPath}/../../../../../../core/boards/evkbimxrt1050/dcd.h"
)

target_include_directories(${MCUX_SDK_PROJECT_NAME} PRIVATE
    ${ProjDirPath}/..
    ${ProjDirPath}/../../../../../../examples/evkbimxrt1050/driver_examples/csi/fragment_gray
    ${ProjDirPath}/../../../../../../core/boards/evkbimxrt1050
)

#path for entry cmake
set(CMAKE_MODULE_PATH
    ${ProjDirPath}/../../../../../../core
)

#Include Entry cmake component
include(all_devices)

# include modules
include(driver_cache_armv7_m7)

include(driver_camera-device-sccb)

include(driver_camera-device-ov7725)

include(driver_camera-device-mt9m114)

include(driver_video-i2c)

include(utility_debug_console_lite)

include(utility_assert_lite)

include(driver_igpio)

include(driver_csi)

include(driver_elcdif)

include(driver_camera-common)

include(driver_video-common)

include(driver_camera-device-common)

include(driver_lpi2c)

include(driver_clock)

include(driver_common)

include(device_CMSIS)

include(component_lpuart_adapter)

include(component_lists)

include(driver_lpuart)

include(device_startup)

include(driver_iomuxc)

include(driver_xip_device)

include(driver_xip_board_evkbimxrt1050)

include(CMSIS_Include_core_cm)

include(utilities_misc_utilities)

include(device_system)


TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--start-group)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE m)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE c)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE gcc)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE nosys)

TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--end-group)


