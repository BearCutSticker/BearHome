# ESP8622 TFT 1.77 inch ESPhome Homeasisstant

## hardware
1. ESP8622
2. TFT 1.77 inch
3. raspberry Pi (ran Homeassistant)
## software
1. Homeassistant <a href="https://www.home-assistant.io/">see</a>
2. esphome <a href="https://esphome.io/">see</a>

## Method
> Connect the circuit pins together like this:

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

<picture>
  <img width="550px" alt="esp8622 and tft 1.77 inch" src="https://bearcutsticker.com/img/esp8622_tft177.png">
</picture>

> NEW DEVICE in ESPhome in Homeasisstant <a href="https://esphome.io/guides/getting_started_hassio.html">refer</a>

Example configuration entry <a href="https://esphome.io/components/display/st7735.html">refer</a>

```ruby
spi:
  clk_pin: GPIO14
  mosi_pin: GPIO13
  miso_pin: GPIO12

display:
  - platform: st7735
    model: "INITR_18BLACKTAB"
    cs_pin: GPIO4
    dc_pin: GPIO5
    rotation: 0
    device_width: 128
    device_height: 160
    col_start: 0
    row_start: 0
    eight_bit_color: true
    update_interval: 1s
```

first a few basics: When setting up a display platform in ESPHome there will be a configuration option called `lambda:` which will be called every time ESPHome wants to re-render the display. In each cycle, the display is automatically cleared before the lambda is executed. You can disable this behavior by setting `auto_clear_enabled: false`. In the lambda, you can write code like in any lambda in ESPHome. Display lambdas are additionally passed a variable called it which represents the rendering engine object. <a href="https://esphome.io/components/display/index.html">refer</a>

```rudy
    pages: 
      - id: page1 
        lambda: |-
          it.strftime(2, 8, id(font1), "%H:%M", id(esptime).now());
          it.image(2, 25, id(my_image));
```

> Addfont

To use fonts you first have to define a font object in your ESPHome configuration file. Just grab a `.ttf`, `.pcf`, or `.bdf` file from somewhere on the internet and place it, for example, inside a fonts folder next to your configuration file.

Next, create a `font:` section in your configuration:
```rudy
font:
  - file: 'Orbitron-VariableFont_wght.ttf'
    id: font1
    size: 15
```
