<!--

import: https://raw.githubusercontent.com/liaTemplates/AVR8js/main/README.md

-->

[![LiaScript](https://raw.githubusercontent.com/LiaScript/LiaScript/master/badges/course.svg)](https://liascript.github.io/course/?https://raw.githubusercontent.com/Supergecki/ino-clock/Inspiration/README.md#1)

# ino-clock
This is a repository for the Arduino lightstrip clock project of the english course for Robotics, Computer Science and Mathematics students at the TU Freiberg.

## Inspiration

## Goal

## Explanation

### Simulation

<div id="matrix-experiment">
<wokwi-neopixel-matrix pin="6" cols="12" rows="1"></wokwi-neopixel-matrix>
<span id="simulation-time"></span>
</div>

```cpp             Automata
#include "FastLED.h"
#define DATA_PIN 6
#define NUM_LEDS 12
#define BRIGHTNESS 180

CRGB leds[NUM_LEDS];

unsigned long second_counter = 0;
int speed = 1; // real seconds per internal second

int hours;
int minutes;
int seconds;
int hour_brightness[] = {128, 255};
int min_sec_brightness[] = {51, 102, 153, 204, 255};

void setup()
{
    FastLED.addLeds<NEOPIXEL, DATA_PIN>(leds, NUM_LEDS);
    FastLED.setBrightness(BRIGHTNESS);
}

void loop()
{
    delay(1000/speed);
    second_counter++; // increase time by 1
    for (int i = 0; i < NUM_LEDS; i++)
    {
        leds[i] = CRGB(0, 0, 0); // Reset all LEDs to apply the new colors afterwards.
    }
    if (second_counter == 86400)
    {
        second_counter = 0; // Full day is gone, reset timer!
    }

    hours = second_counter / 3600;
    minutes = (second_counter % 3600) / 60;
    seconds = (second_counter % 3600) % 60;

    // Set hour LED.
    leds[hours / 2].red = hour_brightness[hours % 2];

    // Set minutes LED.
    leds[minutes / 5].green = min_sec_brightness[minutes % 5];

    // Set seconds LED.
    leds[seconds / 5].blue = min_sec_brightness[seconds % 5];

    FastLED.show();
}
```
@AVR8js.sketch(matrix-experiment)

## Challenges during development

## Future of the project

## Quiz

## Sources
