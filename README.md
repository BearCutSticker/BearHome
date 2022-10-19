# ESP8622 TFT 1.77 inch ESPhome Homeasisstant

## hardward 
1. ESP8622
2. TFT 1.77 inch
3. raspberry Pi (ran Homeassistant)
## softward
1. Homeassistant <a href="https://www.home-assistant.io/">see</a>
2. esphome <a href="https://esphome.io/">see</a>

## Method
Connect the circuit pins together like this:

| TFT PIN       |TFT PIN MARKING|NODEMCU PIN   |ESP PIN       |
| ------------- | ------------- |------------- |------------- |
| 1             | GND           |G             |GND           |
| 2             | VCC           |3V            |3.3V          |
| 3             | SCK           |D5            |GPIO14(HSCLK) |
| 4             | SDA           |D7            |GPIO13(HMOSI) |
| 5             | RES           |D6            |GPIO12(HMISO) |
| 6             | RS            |D1            |GPIO5         |
| 7             | CS            |D2            |GPIO4         |
| 8             | LEDA          |3V            |3.3V          |

