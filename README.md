# ZMK config for Mokulua

This repository contains a minimal configuration to get a [Mokulua][1] working with
nice!nanos and nice!views.

This code is derived from [a fork made by kylemccreery][2], but has been updated for
latest ZMK and modified slightly to remove RGB and to support the nice!view.

The normal OLED definitions have been removed from the shield configuration, but note that
i2c_oled must still be exposed in order for nice_view_adapter to work.

## Hardware mods

The following changes must be made when building the board:

- The usual bodge wire from nice!view's CS pin to the nice!nano's pin 006
- Omit the RAW pin - it must not be connected to the PCB or the n!v will be fried
- Add another bodge wire from the n!n's VCC to the VCC pad of the OLED header
- Not sure if it is absolutely necessary to skip, but I did not solder the two jumpers

## Peripheral encoder

As of right now, encoders on the peripheral side are not supported in mainline ZMK.
However, [there is a PR][3] with which support is added. You can use this branch when
building if you want the peripheral encoder to work.

## Manual build steps

```
west build -p -b nice_nano_v2 -d build/left -- -DSHIELD="mokulua_left nice_view_adapter nice_view" -DZMK_CONFIG="/full/path/to/zmk-config-mokulua/config"
west build -p -b nice_nano_v2 -d build/right -- -DSHIELD="mokulua_right nice_view_adapter nice_view" -DZMK_CONFIG="/full/path/to/zmk-config-mokulua/config"
```

[1]: https://mechwild.com/product/mokulua/
[2]: https://github.com/zmkfirmware/zmk/pull/1297
[3]: https://github.com/zmkfirmware/zmk/pull/1841
