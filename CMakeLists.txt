if(CONFIG_DFU_BSDIFF)

  set(DFU_BSDIFF_PATH ${ZEPHYR_CURRENT_MODULE_DIR}/include)

  zephyr_library()
  zephyr_include_directories(../delta/)

  zephyr_library_sources(
    ${DFU_BSDIFF_PATH}/delta/delta.c
    ${DFU_BSDIFF_PATH}/detools/detools.c
    ${DFU_BSDIFF_PATH}/heatshrink/heatshrink.c
  )

endif()  # CONFIG_DFU_BSDIFF