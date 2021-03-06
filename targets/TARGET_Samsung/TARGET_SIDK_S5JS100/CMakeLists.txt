# Copyright (c) 2020 ARM Limited. All rights reserved.
# SPDX-License-Identifier: Apache-2.0

if(${MBED_TOOLCHAIN} STREQUAL "ARM")
    set(LINKER_FILE device/TOOLCHAIN_ARM_STD/sidk_s5js100.sct)
    set(STARTUP_FILE device/TOOLCHAIN_ARM_STD/startup_sidk_s5js100.S)
elseif(${MBED_TOOLCHAIN} STREQUAL "GCC_ARM")
    set(LINKER_FILE device/TOOLCHAIN_GCC_ARM/sidk_s5js100.ld)
    set(STARTUP_FILE device/TOOLCHAIN_GCC_ARM/startup_sidk_s5js100.S)
endif()

set_property(GLOBAL PROPERTY MBED_TARGET_LINKER_FILE ${CMAKE_CURRENT_SOURCE_DIR}/${LINKER_FILE})

target_include_directories(mbed-core
    INTERFACE
        .
        device
        modem
        security_subsystem
        security_subsystem/drivers
)

target_sources(mbed-core
    INTERFACE
        gpio_api.c
        gpio_irq_api.c
        i2c_api.c
        
        mbed_sdk_init.c
        pinmap.c
        rtc_api.c
        s5js100_dcxo.cpp
        s5js100_pmip.c
        s5js100_pwr.c
        s5js100_watchdog.c
        security_subsystem
        serial_api.c
        serial_dummy_api.c
        serial_pl011_api.c
        serial_usi_api.c
        sleep.c
        spi_api.c
        us_ticker.c
        watchdog_api.c

        device/s5js100_pwrcal.c
        device/s5js100_systemreset.c
        device/sflash_api.cpp
        device/system_core_s5js100.c
        device/system_core_version.c
        device/system_s5js100.c

        security_subsystem/api/trng_api.c

        security_subsystem/drivers/mb_cmd_hash.c
        security_subsystem/drivers/mb_cmd_rng.c
        security_subsystem/drivers/mb_cmd_system.c
        security_subsystem/drivers/sss_driver_rng.c
        security_subsystem/drivers/sss_driver_sha2.c
        security_subsystem/drivers/sss_driver_util.c

        ${STARTUP_FILE}
)
