if(CONFIG_WAMR)

    enable_language (ASM)

    set (WAMR_ROOT_DIR ${CMAKE_CURRENT_SOURCE_DIR}/..)

    zephyr_include_directories(${WAMR_ROOT_DIR}/core/iwasm/include)

    set (WAMR_BUILD_INTERP 1)
    set (WAMR_BUILD_LIBC_BUILTIN 1)
    set (WAMR_BUILD_TARGET "X86_32")
    set (WAMR_BUILD_PLATFORM "zephyr")
    set (WAMR_BUILD_APP_FRAMEWORK 1)
    set (WAMR_BUILD_APP_LIST WAMR_APP_BUILD_BASE)

    include (${WAMR_ROOT_DIR}/build-scripts/runtime_lib.cmake)

    zephyr_library()
    zephyr_library_sources(${WAMR_RUNTIME_LIB_SOURCE})

endif()

