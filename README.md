# ESP32 modbus ABB- B23 and B21
Reading the ABB kWh meter with ESP32 over modbus, publising to Home Assistant

## Hardware
- ESP32 board [lilygo T7-S3  ESP32S3](https://www.lilygo.cc/products/t7-s3)
- TTL to RS485 converter [MAX485](https://www.analog.com/en/products/max485.html)
- kWh meter [B23 112-100](https://new.abb.com/products/2CMA100164R1000/b23-112-100)
- kWh meter [B21 111-100](https://new.abb.com/products/2CMA100149R1000/b21-111-100)


## Software / Documentation
- [Home Assistant](https://www.home-assistant.io/) Home automation software
- [ESPHome](https://esphome.io/) to program the ESP32 (Home Assistant plugin)
- [ABB Modbus documentation (see specific manual][(https://new.abb.com/products/2CMA100149R1000/b21-111-100)

ESPHome config file: [abb_B23_B21.yaml](abb_B23_B21.yaml)



Screenshot from Home Assistant:

![ABB B23_B21  HA](https://github.com/wesdre/esp32_modbus-abb-B23-and-B21/assets/5335971/18e6a514-d70f-4fc5-9440-c2ab6f56183c)

# Thanks to:

systeembeheerder (https://github.com/systeembeheerder) being the sources of inspiration and ABB related code.
fonske (AKA AUijtdehaag) (https://github.com/fonske) For the HW and related code.
