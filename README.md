# Jorne ZMK config

**Inspired by:**
- https://github.com/manna-harbour/miryoku_zmk
- https://github.com/urob/zmk-config

**Keymap editor:**
https://nickcoutsos.github.io/keymap-editor

**Local build:**
```shell
docker run -it --rm \
--security-opt label=disable \
--workdir /jorne-zmk-config \
-v ~/Home/Tools/Keyboard/jorne-zmk-config:/jorne-zmk-config \
-v ~/Home/Tools/Keyboard/firmware:/firmware \
zmkfirmware/zmk-build-arm:4.1-branch /bin/bash

west init -l config && west update
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
