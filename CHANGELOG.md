# Changelog

All notable changes to this Klipper configuration are recorded here.  
Format loosely follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [Unreleased]

- Z offset not yet calibrated
- Input shaper values not yet measured
- Pressure advance at initial estimate (0.04) — not tuned

---

## [0.1.0] — Initial commit

### Added
- Full printer.cfg for BTT SKR 3 EZ with EZ2209 drivers in UART mode
- Cartesian kinematics, 310×310 bed
- BIQU H2 V2S extruder config (rotation_distance: 3.422, gear_ratio: 7:1)
- BLTouch probe with virtual Z endstop
- Dual Z motors with Z_TILT_ADJUST
- Bed mesh (5×5 bicubic)
- ADXL345 input shaper support (values TBD after calibration)
- Filament runout sensor with pause/resume
- NeoPixel light bar (20 LED, GRB)
- Auxiliary fan (independently controlled)
- START_PRINT / END_PRINT macros with slicer parameter passing
- PAUSE / RESUME / CANCEL_PRINT macros
- LED macros: LIGHTS_ON, LIGHTS_OFF, LIGHTS_PRINTING
- Aux fan macros: AUX_FAN_ON, AUX_FAN_OFF
