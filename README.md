# Dogger-mini-game
A minigame made using ESP32 and a 0.96 SSD1306 OLED

This is a minigame to just test your components or for time pass anything you desire

## Components
1x 0.96 OLED White (or your color)
1x ESP32 DEVKIT-V1
1x Joystick Analog
some miscellaneous like Breadboard, jumpers etc..

it's a fun way to test your components instead of the traditional boring programs.

## Pins allocation 
All Vcc&gnd to power supply 
(If you're using Breadboard powersupply make sure it is connected to the same gnd)
OLED (SSD1306 I2C version)


SCL → GPIO 22 (ESP32 default I2C SCL)

SDA → GPIO 21 (ESP32 default I2C SDA)

Joystick module (with VRx, VRy, SW pins)

VRx → GPIO 34 (analog input)

VRy → GPIO 35 (analog input)

SW → GPIO 32 (digital input with pull-up)

## Created under **MIT License**

Copy the program from below 👇: 



## Code

    #include <Wire.h>
    #include <Adafruit_GFX.h>
    #include <Adafruit_SSD1306.h>

    #define SCREEN_WIDTH 128
    #define SCREEN_HEIGHT 64
    Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, -1);


    #define JOY_X 34
    #define JOY_Y 35
    #define JOY_SW 32


    int playerX = 60;
    int playerY = 50;
    const int playerSize = 5;


    int obsX = random(0, SCREEN_WIDTH - 5);
    int obsY = 0;
    const int obsSize = 5;
    int score = 0;

    void setup() {
    Serial.begin(115200);

    if (!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) {
    Serial.println(F("SSD1306 allocation failed"));
    for (;;);
    }
  
    pinMode(JOY_SW, INPUT_PULLUP);

    display.clearDisplay();
    display.setTextColor(SSD1306_WHITE);
    display.setTextSize(1);
    display.setCursor(10, 25);
    display.println("Mini Dodger!");
    display.display();
    delay(1000);
    }

    void loop() {
  
    int xVal = analogRead(JOY_X);
    int yVal = analogRead(JOY_Y);

  
    if (xVal < 1500) playerX -= 1;
    if (xVal > 3000) playerX += 1;
    if (yVal < 1500) playerY -= 1;
    if (yVal > 3000) playerY += 1;

  
    playerX = constrain(playerX, 0, SCREEN_WIDTH - playerSize);
    playerY = constrain(playerY, 0, SCREEN_HEIGHT - playerSize);

   
    obsY += 2;
    if (obsY > SCREEN_HEIGHT) {
    obsY = 0;
    obsX = random(0, SCREEN_WIDTH - obsSize);
    score++;
    }
 
  
    if (playerX < obsX + obsSize && playerX + playerSize > obsX &&
      playerY < obsY + obsSize && playerY + playerSize > obsY) {
    
    display.clearDisplay();
    display.setCursor(25, 25);
    display.setTextSize(1);
    display.print("Game Over Score:");
    display.setCursor(50, 40);
    display.print(score);
    display.display();
    delay(3000);
    score = 0;
    playerX = 60; playerY = 50;
    obsY = 0; obsX = random(0, SCREEN_WIDTH - obsSize);
    }

  
    display.clearDisplay();
    display.fillRect(playerX, playerY,      playerSize, playerSize, SSD1306_WHITE);
    display.fillRect(obsX, obsY, obsSize, obsSize, SSD1306_WHITE);
  
    display.setCursor(0, 0);
    display.setTextSize(1);
    display.print("Score:");
    display.print(score);
    display.display();

    delay(10);
    }



