#include "Adafruit_NeoPixel.h"

#define PIXEL_PIN     D5
#define PIXEL_COUNT   10
#define PIXEL_TYPE    NEO_GRB + NEO_KHZ800

Adafruit_NeoPixel strip = Adafruit_NeoPixel(PIXEL_COUNT, PIXEL_PIN, PIXEL_TYPE);

void setup() {

  // start the serial connection
  Serial.begin(115200);
  
  // neopixel init
  strip.begin();
  strip.show();

}

void loop() {
  // sensor aanroepen.
  int waterValue = analogRead(A0);
  Serial.println(waterValue);
  delay(100);

  if (waterValue < 293) {
          colorWipe(strip.Color(0, 0, 255), 0); //
        } else {
          colorWipe(strip.Color(255, 0, 0), 0); // 
        }
}

void colorWipe(uint32_t c, uint8_t wait) {
  for(uint16_t i=0; i<strip.numPixels(); i++) {
    strip.setPixelColor(i, c);
    strip.show();
    delay(wait);
  }
}
