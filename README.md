# Water sensor

In this file I will explain how you can check if there is still enough water in the bowl of your pet. When there is enough water we want to give our led strip a blue color, is the bowl empty we want a red color. To control the LED strip we will work with Adafruit_Neopixel library. 

## Installing

Before we start you need an Arduino board and the Arduino software.
- I used the Arduino 1.8.7 software on Mac OS X 10.8 Mountain Lion or newer
- For Windows check there website https://www.arduino.cc/en/main/software

When you have installed the Arduino software look for your **NodeMCU board**.

**Tools** --> **Board:NodeMCU 1.0** 

Than check if you selected the right **Port**.

### Install Adafruit_NeoPixel Library
We work with the AdaFruit_NeoPixel because controlling NeoPixels from scratch is quite a challange. 
So they provided us with a library. (The librabry works with most mainstram Arduino boards; *Uno, Mega, Leonardo, Micro, Adafruit Flora,* etc.


Go to **Sketch** --> **Include Library** --> **Manage Libraries...**

In the text input box type in **"NeoPixel"**. Look for **"Adafruit NeoPixel by Adafruit"** and select the latest version by clicking on the popup menu next to the **Install** button. Then click on the **Install** button. After it's installed, you can click the **"close"** button.

## Let's Start

#### Step 1: The necessary components
1. Like I said before; the Arduino board
2. The water sensor
3. The LED strip 

#### Step 2: Connect the components
##### Water Sensor:
- Connect the **5v** on the Arduino to **+** on the water sensor
- Connect the **GND** on the Arduino to **-** on the water sensor
- Connect the **A0** on the Arduino to **s** on the water sensor
##### Led Strip:
- Connect the **GND** on the Arduino to **GND** on the led strip
- Connect the **D5** on the Arduino to **Do/Din** on the led strip
- Connect the **3V** on the Arduino to **5V** on the led strip

#### Step 3: Time for the code

First we want to include the header file of NeoPixel.
```
#include <Adafruit_NeoPixel.h>
```




```
void setup(){
 
Serial.begin(9600);
 
}
 
void loop(){
 
Serial.print("Water level Sensor Value:");
Serial.println(analogRead(A5));
delay(100);
 
}
```
