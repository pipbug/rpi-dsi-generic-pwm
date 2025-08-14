# 📟 rpi-dsi-generic-pwm

**A Raspberry Pi Device Tree Overlay for generic DSI displays** that are similar to the official RPi 7" display, but require a **separate PWM signal** from the GPIO header for backlight control.

This overlay is based on [`vc4-kms-dsi-7inch-overlay`](https://github.com/raspberrypi/linux) from the Raspberry Pi kernel, modified for **PWM backlight control** on **GPIO18** (physical pin 12).

---

## ✨ Features
- Works with most generic DSI panels that expect a separate PWM backlight input.
- Based on official Raspberry Pi overlay for compatibility.
- Easy to install and configure.

---

## 📋 Requirements
- Raspberry Pi with DSI interface
- DSI display that uses external PWM for backlight
- GPIO18 (physical pin 12) free for PWM output  
  _(Ensure **PWM0** is not in use — e.g. disable PWM audio.)_

---

## 🚀 Installation

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
