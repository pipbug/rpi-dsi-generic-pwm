# rpi-dsi-generic-pwm

**A Raspberry Pi Device Tree Overlay for generic DSI displays** that are similar to the official RPi 7" display, but require a **separate PWM signal** from the GPIO header for backlight control.

This overlay is based on [`vc4-kms-dsi-7inch-overlay`](https://github.com/raspberrypi/linux) from the Raspberry Pi kernel, modified for **PWM backlight control** on **GPIO18** (physical pin 12).


## Features
- Works with most generic DSI panels that expect a separate PWM backlight input.
- Based on official Raspberry Pi overlay for compatibility.
- Easy to install and configure.


## Requirements
- GPIO18 (physical pin 12) free for PWM output  
  _(Ensure **PWM0** is not in use — e.g. disable PWM audio.)_
- DSI display with PWM pin available. [Some models require you to move a 0-ohm resistor before connecting the PWM wire to the corresponding pad.](https://i.imgur.com/he4CV9k.jpeg)

## Installation

```bash
# 1. Become root
sudo -i

# 2. Download the overlay source
wget https://raw.githubusercontent.com/pipbug/rpi-dsi-generic-pwm/main/rpi-dsi-generic-pwm.dts

# 3. Compile the overlay
dtc -@ -I dts -O dtb -o rpi-dsi-generic-pwm.dtbo rpi-dsi-generic-pwm.dts

# 4. Copy to overlays folder
cp rpi-dsi-generic-pwm.dtbo /boot/firmware/overlays/

# 5. Enable in config.txt
echo "dtoverlay=rpi-dsi-generic-pwm" >> /boot/firmware/config.txt
echo "dtparam=audio=off" >> /boot/firmware/config.txt

# 6. Reboot
reboot
```


## Confirmed Working Displays

* **ALLNET China 5-inch DSI LCD MIPI Display (capacitive touch, 800×480)**
  [🔗 Product page](https://shop.allnetchina.cn/products/5inch-dsi-lcd-mipi-display-with-capacitive-touch-screen)

  _Contribute to this project by testing your display and let everyone know how it works!_


## License

This project is licensed under the [Raspberry Pi Linux license](https://github.com/raspberrypi/linux/blob/rpi-6.12.y/COPYING).


## Notes

* If PWM audio is enabled, it will block usage of PWM0. Disable it before using this overlay.
* Tested on Raspberry Pi OS Bookworm with kernel 6.12.
* This overlay was tested with displays electrically similar to the official Raspberry Pi 7" display but requiring an external PWM input for backlight brightness.
