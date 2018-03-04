# Adafruit_SGP30

This is a port of the library developed by Adafruit for the Adafruit SGP30 Gas / Air Quality I2C sensor breakout. This port/wrap enables the sensor to be used on a particle.io device.

This chip/breakout uses I2C to communicate. 2 pins are required to interface with the photon (D0 to SDA and D1 to SCL). You will also need to add power (3v3/GND).

The breakout can be sourced here: http://www.adafruit.com/products/3709

The original hook-up guide here: https://learn.adafruit.com/adafruit-sgp30-gas-tvoc-eco2-mox-sensor

The original library developed by Adafruit can be sourced here: https://github.com/adafruit/Adafruit_SGP30

The Fritzing resources can be sourced here: https://github.com/adafruit/Fritzing-Library

#

This library was modified/wrapped by https://github.com/dyadica in order to work with Particle Photon & Core.

## Usage

Connect SGP30 hardware to the photon via the I2C ports, add the Adafruit_SGP30 library to your project. The sensor can be polled via the following code:

```
#include "Adafruit_SGP30.h"
Adafruit_SGP30 adafruit_SGP30;

void setup()
{
  Serial.begin(9600);
  Serial.println("SGP30 test");

  if (! adafruit_SGP30.begin()){
    Serial.println("Sensor not found :(");
    while (1);
  }
}

void loop()
{
  if (! adafruit_SGP30.IAQmeasure())
  {
    Serial.println("Measurement failed");
    return;
  }

  Serial.print("TVOC "); Serial.print(adafruit_SGP30.TVOC); Serial.print(" ppb\t");
  Serial.print("eCO2 "); Serial.print(adafruit_SGP30.eCO2); Serial.println(" ppm");
  delay(1000);
}

```
For a more in-depth example, including how to calibrate the sensor; please see the example sgp30test.ino within the examples/usage folder.

## License Information

This code was originally developed by Adafruit and as such adopts their license policy:

This is the Adafruit SGP30 Gas / Air Quality I2C sensor library

Tested and works great with the Aadafruit SGP30 Breakout Board

http://www.adafruit.com/products/3709
This chip uses I2C to communicate, 2 pins are required to interface

Adafruit invests time and resources providing this open source code, please support Adafruit and open-source hardware by purchasing products from Adafruit!

Written by Limor Fried for Adafruit Industries.
BSD license, check license.txt for more information All text above must be included in any redistribution.

# Useful Information

Please note, this sensor, like all VOC/gas sensors, has variability and to get precise measurements you will want to calibrate it against known sources! The following information sourced via the internet can be used provide a general outline as to what the reported values mean.

## C02 Levels

C02 Levels as taken from: https://www.kane.co.uk/knowledge-centre/what-are-safe-levels-of-co-and-co2-in-rooms

250-350ppm	Normal background concentration in outdoor ambient air

350-1,000ppm	Concentrations typical of occupied indoor spaces with good air exchange.

1,000-2,000ppm	Complaints of drowsiness and poor air.

2,000-5,000 ppm	Headaches, sleepiness and stagnant, stale, stuffy air. Poor concentration, loss of attention, increased heart rate and slight nausea may also be present.

5,000	Workplace exposure limit (as 8-hour TWA) in most jurisdictions.

Greater than 40,000 ppm	Exposure may lead to serious oxygen deprivation resulting in permanent brain damage, coma, even death.

## TVOC Levels

TVOC Levels as taken from: http://www.critical-environment.com/blog/know-the-air-you%E2%80%99re-breathing-volatile-organic-compound-2-of-4/

Less than 200 µg/m3	No irritation or discomfort expected

200 – 3,000 µg/m3	Irritation and discomfort may be possible

3,000 – 25,000 µg/m3	Discomfort expected and headache possible

Greater than 25,000 µg/m3	Toxic range where other neurotoxic effects may occur
