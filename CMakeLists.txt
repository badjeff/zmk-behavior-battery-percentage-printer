zephyr_library()

if ((NOT CONFIG_ZMK_SPLIT) OR CONFIG_ZMK_SPLIT_ROLE_CENTRAL)
  zephyr_library_sources_ifdef(CONFIG_ZMK_BEHAVIOR_BATT_PCT_PRINTER src/behavior_battery_percentage_printer.c)
  zephyr_include_directories(${APPLICATION_SOURCE_DIR}/include)
endif()
