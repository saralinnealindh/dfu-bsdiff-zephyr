if(CONFIG_DFU_BSDIFF)

  set(DFU_BSDIFF_PATH ${ZEPHYR_CURRENT_MODULE_DIR})

  zephyr_library()
  zephyr_include_directories(${DFU_BSDIFF_PATH}/include)

  zephyr_library_sources(
    ${DFU_BSDIFF_PATH}/delta/delta.c
    ${DFU_BSDIFF_PATH}/detools/detools.c
    ${DFU_BSDIFF_PATH}/heatshrink/heatshrink_decoder.c
  )

endif()  # CONFIG_DFU_BSDIFF