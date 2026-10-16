# ABB B23 / B21 kWh meters – Modbus registers used

The registers read by the ESPHome configuration in this repository. Addresses,
data types and resolutions follow the ABB Modbus manual for the B-series
meters (EQ meters); see the documentation links on the product pages:

- [B23 112-100](https://new.abb.com/products/2CMA100164R1000/b23-112-100) – 3-phase
- [B21 111-100](https://new.abb.com/products/2CMA100149R1000/b21-111-100) – 1-phase

The manual lists many more registers (reactive and apparent energy and power,
per-tariff values, quadrants and more). Only the ones below are used here.

## Connection

| | |
|---|---|
| Physical layer | RS485, both meters on one bus (daisy chain) |
| Protocol | Modbus RTU |
| Serial settings in this setup | 9600 baud, 8 data bits, no parity, 1 stop bit |
| Addresses in this setup | B23 = 1, B21 = 2 |
| Function code | 03, read holding registers |

Baud rate, parity and address are set in the meter's own menu. They have to
match the `uart` and `modbus_controller` settings in the ESPHome configuration.

## Data types

| Type | Registers | Notes |
|---|---|---|
| U_WORD | 1 | unsigned 16 bit |
| U_DWORD / S_DWORD | 2 | unsigned / signed 32 bit, high word first |
| U_QWORD | 4 | unsigned 64 bit, high word first |

A value the meter does not support or cannot measure is returned with all bits
set (`0xFFFF…`).

## Energy

| Address | Meter | Value | Type | Resolution | Unit |
|---|---|---|---|---|---|
| 0x5000 | B23, B21 | Active import energy, total | U_QWORD | 0.01 | kWh |
| 0x5004 | B23, B21 | Active export energy, total | U_QWORD | 0.01 | kWh |
| 0x5460 | B23 | Active import energy, L1 | U_QWORD | 0.01 | kWh |
| 0x5464 | B23 | Active import energy, L2 | U_QWORD | 0.01 | kWh |
| 0x5468 | B23 | Active import energy, L3 | U_QWORD | 0.01 | kWh |
| 0x546C | B23 | Active export energy, L1 | U_QWORD | 0.01 | kWh |
| 0x5470 | B23 | Active export energy, L2 | U_QWORD | 0.01 | kWh |
| 0x5474 | B23 | Active export energy, L3 | U_QWORD | 0.01 | kWh |

## Instantaneous values

| Address | Meter | Value | Type | Resolution | Unit |
|---|---|---|---|---|---|
| 0x5B00 | B23, B21 | Voltage L1-N | U_DWORD | 0.1 | V |
| 0x5B02 | B23 | Voltage L2-N | U_DWORD | 0.1 | V |
| 0x5B04 | B23 | Voltage L3-N | U_DWORD | 0.1 | V |
| 0x5B0C | B23, B21 | Current L1 | U_DWORD | 0.01 | A |
| 0x5B0E | B23 | Current L2 | U_DWORD | 0.01 | A |
| 0x5B10 | B23 | Current L3 | U_DWORD | 0.01 | A |
| 0x5B14 | B23, B21 | Active power, total | S_DWORD | 0.01 | W |
| 0x5B16 | B23 | Active power, L1 | S_DWORD | 0.01 | W |
| 0x5B18 | B23 | Active power, L2 | S_DWORD | 0.01 | W |
| 0x5B1A | B23 | Active power, L3 | S_DWORD | 0.01 | W |
| 0x5B2C | B23, B21 | Frequency | U_WORD | 0.01 | Hz |
| 0x5B3A | B23, B21 | Power factor, total | U_WORD | 0.001 | – |

Active power is signed: negative means export.

## Identification

| Address | Meter | Value | Read as |
|---|---|---|---|
| 0x8900 | B23, B21 | Serial number | 6 bytes, shown as hex |
| 0x8908 | B23, B21 | Firmware version | 16 bytes, ASCII |
| 0x8960 | B23, B21 | Type designation | 8 bytes, ASCII |

These do not change, so the configuration reads them only every 60th poll.
