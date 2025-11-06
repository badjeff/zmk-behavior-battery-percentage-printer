# ZMK Batter Percentage Printer Behavior

This is a modified version of [alan0ford's behavior_battery_printer.c](https://github.com/alan0ford/zmk-lplancks/blob/GHPilotBatt/boards/shields/lplancks/behavior_battery_printer.c). Changes has been added to make the behavior awaring of peripheral id.

## What it does

Type the battery percentage by triggering behaviors on the sheild's keymap.

To report battery state of peripheral sheild, you can use combo-keys to toggle an utility layer and assign this behavior on a layer, the dongle would report the peripheral battery state in percentage by sending keycodes (e.g. '89% ') to the host.

## Installation

Include this project on your ZMK's west manifest in `config/west.yml`:

```diff
  [...]
  remotes:
+    - name: badjeff
+      url-base: https://github.com/badjeff
  projects:
+    - name: zmk-behavior-battery-percentage-printer
+      remote: badjeff
+      revision: main
  [...]
```

And update `shield.conf` on both *central* and *peripheral* shields.
```
CONFIG_ZMK_SPLIT_BLE_CENTRAL_BATTERY_LEVEL_FETCHING=y
```

Now, update your `shield.keymap` adding the behaviors.

```c
/{
#include <behaviors/battery_percentage_printer.dtsi>

        keymap {
                compatible = "zmk,keymap";
                base {
                        bindings = <
                              ...
                              ...   &bapp   ...   &bapp ...
                                  /* left */    /* right */
                              ...
                        >;
                };
       };

};
```
