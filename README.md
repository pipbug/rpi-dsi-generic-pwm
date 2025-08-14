# rpi-dsi-generic-pwm
Raspberry Pi device tree overlay for use with generic DSI displays similar to the RPi 7" display but that rely on a separate PWM signal from the GPIO header for backlight control.
Overlay based upon vc4-kms-dsi-7inch-overlay from the RPi kernel but modified for PWM backlight control on GPIO18 (physical pin 12).

How to install:

sudo -i
dtc -@ -I dts -O dtb -o rpi-dsi-generic-pwm.dtbo rpi-dsi-generic-pwm.dts

cp rpi-dsi-generic-pwm.dtbo /boot/firmware/overlays/rpi-dsi-generic-pwm.dtbo

echo "dtoverlay=rpi-dsi-generic-pwm" >> /boot/firmware/config.txt

reboot

https://github.com/pipbug/rpi-dsi-generic-pwm
