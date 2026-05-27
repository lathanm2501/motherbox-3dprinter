# Bill of Materials — Electronics
### 310x310 Bed Slinger 3D Printer

Last Updated: 2026-05-27

---

## Controllers & Compute

| Item | Qty | Specs / Notes |
|---|---|---|
| BTT SKR 3 EZ mainboard | 1 | Main printer MCU, STM32H743, EZ driver sockets |
| Raspberry Pi 3B+ | 1 | Klipper host, running Mainsail/Fluidd + KlipperScreen |
| Raspberry Pi Pico (RP2040) | 1 | Secondary MCU — dual ADXL345, connected to Pi via USB |
| BTT EZ2209 stepper drivers | 5 | X, Y, Z, Z1, Extruder — seated in SKR EZ sockets |

---

## Power

| Item | Qty | Specs / Notes |
|---|---|---|
| Switching power supply | 1 | 24V 20A 480W, AC 110/220V universal input |
| AC inlet module | 1 | IEC320 C14, 10A 250V, integrated rocker switch — verify fuse rating (5A or 6.3A recommended) |
| Buck converter — XY-3606 | 1 | 24V → 5.2V 6A, powers Pi 3+ via GPIO; Pico powered via Pi USB port |

---

## Motion — Stepper Motors

| Item | Qty | Specs / Notes |
|---|---|---|
| Creality Original 42-40 stepper motor | 4 | NEMA 17, 1.8° step angle, 2-phase, 0.4N.m holding torque, 1A rated current, 5mm D-shaft, 42×42×40mm — X (1), Y (1), Z×2 |
| Y-axis upgrade motor | TBD | Target 0.55–0.65N.m, 48mm body — e.g. LDO-42STH48-2004AC or equivalent; evaluate after first prints |

---

## Print Head

| Item | Qty | Specs / Notes |
|---|---|---|
| BIQU H2 V2S direct drive extruder | 1 | Integrated stepper + hotend, 7:1 gear ratio, rotation_distance 3.422 |
| BLTouch probe | 1 | Auto bed leveling, Z virtual endstop |

---

## Bed

| Item | Qty | Specs / Notes |
|---|---|---|
| Heated bed — wire element | 1 | 310×310mm, 24V |
| Bed thermistor | 1 | EPCOS 100K B57560G104F or equivalent — verify type |
| External MOSFET board | 1 | HYG025N06LS1P MOSFET (60V/90A), offloads bed heater current from SKR — signal from SKR HB headers, 24V in/out direct to PSU and bed |

---

## Sensors & Inputs

| Item | Qty | Specs / Notes |
|---|---|---|
| Filament runout sensor | 1 | Switch type, wired to PC2 |
| Mechanical endstop | 2 | X axis (PC1), Y axis (PC3) |
| NC momentary pushbutton | 1 | Emergency stop, wired to Z-STOP header (PC0) — must be normally-closed |
| ADXL345 accelerometer board | 2 | Toolhead (Pico SPI0: GP2/3/4/5) + Bed (Pico SPI1: GP10/11/12/13) |

---

## Accessories & Peripherals

| Item | Qty | Specs / Notes |
|---|---|---|
| WS2812B NeoPixel LED strip | 1 | 20 LEDs, GRB color order, wired to PE6 |
| Touchscreen display | 1 | 5" IPS DSI, 800×480, capacitive touch, MIPI DSI, driver-free — running KlipperScreen |
| USB webcam | 1 | Logitech C200 — running via Crowsnest |
| Hotend heatsink fan | 1 | Always-on when hotend >50°C, wired to PB6 |
| Part cooling fan — primary | 1 | Slicer-controlled, wired to PB7 |
| Part cooling fan — auxiliary | 1 | Macro-controlled (AUX_FAN_ON/OFF), wired to PB5 |
| Electronics box ventilation fan | 1 | 40mm 24V, always-on, wired to uncontrolled fan header on SKR 3 EZ |

---

## Connectors & Cabling

| Item | Qty | Specs / Notes |
|---|---|---|
| USB-A female panel mount | 2 | Pi enclosure side — 1× Pico connection, 1× webcam |
| Micro-USB or USB-C female panel mount | 1 | Pico enclosure side — connects to Pi via USB cable |

---

## Outstanding / TBD

- Y-axis upgrade motor — evaluate after first prints; upgrade if layer shifting or motor heat is observed
- Fuse rating on AC inlet module — verify installed fuse is 5A or 6.3A
- MOSFET board heatsink — fit a heatsink if available; ensure airflow from electronics box fan reaches it
- 3D printed parts audit — pending (multiple bracket versions across project files, requires physical measurement)
