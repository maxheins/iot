## Automatic Pet Feeder with Arduino 

We want to build an automatic pet feeder with **Arduino**. In this file I will explain how to check if there is still enough water in the bowl of your pet. 

### Let's start

Before we start you need an Arduino board and the Arduino software.
- I used the Arduino 1.8.7 on Mac OS X 10.8 Mountain Lion or newer
- For Windows check this website https://www.arduino.cc/en/main/software

#### Step 1: Necessary components
1. Like I said; the Arduino
2. 4 wires 
3. water sensor

#### Step 2: Connect the components
- Connect the **5v** on the Arduino to the **+** on the water sensor
- Connect the **GRND** on the Arduino to the **-** on the water sensor
- Connect the **A5** on the Arduino to he **s** on the water sensor

### Step 3: Time for the code

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
