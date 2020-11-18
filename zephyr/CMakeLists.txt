if(CONFIG_WAMR)
    zephyr_interface_library_named(wamr)

    enable_language (ASM)

    set (WAMR_ROOT_DIR ${CMAKE_CURRENT_SOURCE_DIR}/..)

    set (WAMR_BUILD_AOT 1)
    set (WAMR_BUILD_LIBC_BUILTIN 1)
    set (WAMR_BUILD_TARGET "X86_32")
    set (WAMR_BUILD_PLATFORM "zephyr")
    set (WAMR_BUILD_APP_FRAMEWORK 1)
    set (WAMR_BUILD_APP_LIST WAMR_APP_BUILD_BASE)
    set (CMAKE_BUILD_TYPE Debug)

    include (${WAMR_ROOT_DIR}/build-scripts/runtime_lib.cmake)

    zephyr_library()
    zephyr_include_directories(wamr INTERFACE
        ${WAMR_ROOT_DIR}/core/iwasm/include
        ${WAMR_ROOT_DIR}/core/shared/platform/include
        ${WAMR_ROOT_DIR}/core/app-mgr/app-mgr-shared
        ${WAMR_ROOT_DIR}/core/app-framework/app-native-shared
        ${WAMR_ROOT_DIR}/core/shared/utils
        ${WAMR_ROOT_DIR}/core/shared/platform/zephyr/
        ${WAMR_ROOT_DIR}/core/app-framework/base/native
        ${WAMR_ROOT_DIR}/core/app-framework/base/app/wa-inc
    )
    zephyr_library_sources(PRIVATE ${WAMR_RUNTIME_LIB_SOURCE})

    zephyr_library_link_libraries(wamr)

endif()
