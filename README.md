# zmk-config-jorne

This is the official Jorne config for the ZMK keymap editor

* This config was built with: https://nickcoutsos.github.io/keymap-editor (use it to modify keymap)
* Keymap editor source code: https://github.com/nickcoutsos/keymap-editor
* Also see https://github.com/joric/nrfmicro/wiki


```shell
docker run -it --rm \
--security-opt label=disable \
--workdir /jorne-zmk-config \
-v ~/Home/Tools/Keyboard/jorne-zmk-config:/jorne-zmk-config \
-v ~/Home/Tools/Keyboard/firmware:/firmware \
zmkfirmware/zmk-build-arm:4.1-branch /bin/bash

west init -l config && west updates
west zephyr-export


west build -d build/left -p always -s zmk/app -b nice_nano_v2 -- \
-DSHIELD=jorne_left \
-DZMK_CONFIG=/jorne-zmk-config/config

west build -d build/right -p always -s zmk/app -b nice_nano_v2 -- \
-DSHIELD=jorne_right \
-DZMK_CONFIG=/jorne-zmk-config/config

cp /jorne-zmk-config/build/left/zephyr/zmk.uf2 /firmware/jorne_left.uf2
cp /jorne-zmk-config/build/right/zephyr/zmk.uf2 /firmware/jorne_right.uf2
```
