# Dogger-mini-game
A minigame made using ESP32 and a 0.96 SSD1306 OLED

This is a minigame to just test your components or for time pass anything you desire

Here the components used are 
1x 0.96 OLED
1x ESP32 DEVKIT-V1
1x Joystick Analog
some miscellaneous like Breadboard, jumpers etc..

it's a fun way to test your components instead of the traditional boring programs.

Pins allocation:
All Vcc&gnd to power supply 
(If you're using Breadboard powersupply make sure it is connected to the same gnd)
OLED (SSD1306 I2C version)


SCL → GPIO 22 (ESP32 default I2C SCL)

SDA → GPIO 21 (ESP32 default I2C SDA)

Joystick module (with VRx, VRy, SW pins)

VRx → GPIO 34 (analog input)

VRy → GPIO 35 (analog input)

SW → GPIO 32 (digital input with pull-up)



