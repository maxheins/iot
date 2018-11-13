# Water sensor

In this file I will explain how you can check if there is still enough water in the bowl of your pet. When there is enough water we want to give our led strip a blue color, is the bowl empty we want a red color. To control the LED strip we will work with Adafruit_Neopixel library. 

## Installing

Before we start you need an Arduino board and the Arduino software.
- I used the Arduino 1.8.7 software on Mac OS X 10.8 Mountain Lion or newer
- For Windows check there website https://www.arduino.cc/en/main/software

When you have installed the Arduino software look for your **NodeMCU board**.

**Tools** > **Board:NodeMCU 1.0**

Than check if you selected the right **Port**.


## Install Adafruit_NeoPixel Library
We work with the AdaFruit_NeoPixel because controlling NeoPixels from scratch is quite a challange. 
So they provided us with a library. (The librabry works with most mainstram Arduino boards; *Uno, Mega, Leonardo, Micro, Adafruit Flora,* etc.


Go to **Sketch** > **Include Library** > **Manage Libraries...** 

In the text input box type in **"NeoPixel"**. Look for **"Adafruit NeoPixel by Adafruit"** and select the latest version by clicking on the popup menu next to the **Install** button. Then click on the **Install** button. After it's installed, you can click the **"close"** button.

## Let's Start

#### Step 1: The necessary components
1. Like I said before; the Arduino board

![nodemcu_v31](https://user-images.githubusercontent.com/45005992/48438606-9ff2f800-e784-11e8-9069-c8e20df16755.png)

2. The water sensor

![water-level-sensor-500x500](https://user-images.githubusercontent.com/45005992/48438602-9b2e4400-e784-11e8-8332-8d228c97539f.png)

3. The LED strip 

![ml-smdf-rgbw](https://user-images.githubusercontent.com/45005992/48438604-9d909e00-e784-11e8-9a86-a58213be5896.png)

4. Six wires

![wires](https://user-images.githubusercontent.com/45005992/48438829-27406b80-e785-11e8-80bc-1f59be195a8b.png)


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
Open a new blank file in Arduino.

First we want to include the header file of NeoPixel.
```
#include <Adafruit_NeoPixel.h>
```

Than we want to define the pin of the Arduino who is connected to the **led strip**.
As you can see that is **D5**.

We count **10**, cause I use a led strip with 10 ligths. (if u use more ligths, change the number)

The pixel type is going to be RGB.

```
#define PIXEL_PIN     D5
#define PIXEL_COUNT   10
#define PIXEL_TYPE    NEO_GRB + NEO_KHZ800
```

The next line declares a NeoPixel object. We will refer to this by name later to control the strip of pixels. There are three parameters or arguments in the parentheses. These are the one we just defined. 

```
Adafruit_NeoPixel strip = Adafruit_NeoPixel(PIXEL_COUNT, PIXEL_PIN, PIXEL_TYPE);
```

Then in the **setup()** function we start the serial connection and call **begin()** to prepare the data pin for the NeoPixel output.

```
void setup() {

  // start the serial connection
  Serial.begin(115200);
  
  // neopixel init
  strip.begin();
  strip.show();

}
```
The loop() function does precisely what it's name suggests, and loops consecutively, allowing your program to change and respond. 

Now in the loop() we are connecting the **water sensor** to the code. Which is connected to A0.
We give it a name; **waterValue**. 


```
void loop() {
  // sensor aanroepen.
  int waterValue = analogRead(A0);
  Serial.println(waterValue);
  delay(100);
```

Then we build an **if statement**. When you put your water sensor in a glass of water it will give the value; **293**. 
So when the WaterValue is lower than 293 we want to change the color to red.

And when the number is 293 it will give the color blue.

(Does your water sensor gives an other value, change it to that number)
```
  if (waterValue < 293) {
          colorWipe(strip.Color(0, 0, 255), 0); //color red
        } else {
          colorWipe(strip.Color(255, 0, 0), 0); //color blue
        }
}
```

And as last the colorWipe. 
The ColorWipe function paints a color, one pixel at a time, over the length of the strip.  

```
void colorWipe(uint32_t c, uint8_t wait) {
  for(uint16_t i=0; i<strip.numPixels(); i++) {
    strip.setPixelColor(i, c);
    strip.show();
    delay(wait);
  }
}
```

