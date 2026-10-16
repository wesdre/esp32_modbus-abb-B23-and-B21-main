# ESP32 Modbus ABB B23 and B21

Reading the **ABB B23** (3-phase) and **ABB B21** (1-phase) kWh meters with an
ESP32 over RS485 / Modbus RTU and publishing them to Home Assistant with
ESPHome.

| Folder | Contents |
|---|---|
| [`esphome/`](esphome/) | ESPHome configuration, wiring and a Home Assistant screenshot |
| [`documents/`](documents/) | [Modbus registers used for the B23 and B21](documents/ABB-B23-B21-modbus-registers.md) |

## In short

- Both meters on one RS485 bus, B23 at address 1 and B21 at address 2
- Modbus RTU, 9600 8N1, function code 03
- Energy (import/export, per phase), voltage, current, power, frequency and
  power factor
- Uses ESPHome's standard `modbus_controller`

## Thanks to

- [systeembeheerder](https://github.com/systeembeheerder) – source of
  inspiration and the ABB related code
- [fonske (AKA AUijtdehaag)](https://github.com/fonske) – the hardware and
  related code

## License

[GPL-3.0](LICENSE)
