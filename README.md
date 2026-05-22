# Klipper Config — BTT SKR 3 EZ / 310×310 Cartesian

Personal Klipper configuration for a cartesian bed-slinger with a BIQU H2 V2S direct drive extruder and BLTouch probe. Maintained here for version control, backup, and reference.

---

## Hardware

| Component | Details |
|---|---|
| Board | BigTreeTech SKR 3 EZ |
| Drivers | EZ2209 (UART mode) |
| Kinematics | Cartesian (bed slinger) |
| Bed | 310 × 310 mm heated |
| Extruder | BIQU H2 V2S Direct Drive |
| Hotend | Compatible with H2 V2S (max 300°C) |
| Probe | BLTouch |
| Z axis | Dual motor, T8 leadscrew |
| Accelerometer | ADXL345 (SPI, for input shaper) |
| Filament Sensor | Mechanical switch |
| LEDs | NeoPixel light bar (WS2812B GRB, 20 LEDs) |
| Aux Fan | Independently controlled |

---

## Klipper Version

> **Pin this before deploying to a new install.**  
> Run `git -C ~/klipper log --oneline -1` on your host and record the commit hash here.

```
Klipper commit: <fill in after flashing>
Moonraker version: <fill in>
```

Config syntax changes between Klipper releases. If this config fails to load on a fresh install, check the Klipper changelog for breaking changes since the pinned commit above.

---

## Key Calibration Values

These are tuned per-machine and will differ from defaults. Update this table after each calibration run.

| Parameter | Value | Notes |
|---|---|---|
| `rotation_distance` (extruder) | 3.422 | H2 V2S — verify with 100mm extrusion test |
| `pressure_advance` | 0.04 | Starting point — tune with PA tower |
| `z_offset` | _not set_ | Run `PROBE_CALIBRATE` after first setup |
| `shaper_type_x` / `shaper_freq_x` | _not set_ | Run `SHAPER_CALIBRATE` |
| `shaper_type_y` / `shaper_freq_y` | _not set_ | Run `SHAPER_CALIBRATE` |

---

## Pins to Verify Before First Power-On

The following pins are marked `# VERIFY` in the config. Cross-reference with your physical wiring and the [BTT SKR 3 EZ pinout diagram](https://github.com/bigtreetech/SKR-3) before powering on.

- `[bltouch]` — `sensor_pin`, `control_pin`
- `[fan]` — part cooling fan pin
- `[heater_fan hotend_fan]` — heatsink fan pin
- `[fan_generic aux_fan]` — aux fan pin
- `[filament_switch_sensor]` — switch pin
- `[neopixel light_bar]` — data pin
- `[extruder]` / `[heater_bed]` — thermistor types (`sensor_type`)

---

## First-Time Setup (in order)

1. Flash Klipper firmware to the SKR 3 EZ (STM32H743, USB)
2. Find your serial ID: `ls /dev/serial/by-id` — update `[mcu] serial:` in `printer.cfg`
3. Copy `printer.cfg` to `~/printer_data/config/`
4. Power on — check for Klipper errors in the web UI
5. Test motor directions:
   ```
   STEPPER_BUZZ STEPPER=stepper_x
   STEPPER_BUZZ STEPPER=stepper_y
   STEPPER_BUZZ STEPPER=stepper_z
   STEPPER_BUZZ STEPPER=stepper_z1
   ```
   Flip `dir_pin` polarity (add/remove `!`) if any axis moves the wrong direction.
6. Home X and Y only first: `G28 X Y`
7. Manually bring nozzle close to bed, then home Z: `G28 Z`
8. Level dual Z: `Z_TILT_ADJUST`
9. Calibrate Z offset: `PROBE_CALIBRATE`
10. Generate bed mesh: `BED_MESH_CALIBRATE`
11. Calibrate extruder: 100mm extrusion test → update `rotation_distance`
12. Tune Pressure Advance using a PA tower print
13. Run input shaping:
    ```
    TEST_RESONANCES AXIS=X
    TEST_RESONANCES AXIS=Y
    SHAPER_CALIBRATE
    SAVE_CONFIG
    ```

---

## Slicer Start / End G-code

**Start G-code:**
```
START_PRINT BED_TEMP={material_bed_temperature_layer_0} EXTRUDER_TEMP={material_print_temperature_layer_0}
```

**End G-code:**
```
END_PRINT
```

---

## Probe Offset

The BLTouch is offset from the nozzle. Measure physically and update in `[bltouch]`:

```
x_offset: -30   # probe is 30mm left of nozzle
y_offset: -10   # probe is 10mm forward of nozzle
```

The `[safe_z_home]` position and `[bed_mesh]` min/max account for these offsets.

---

## Notes

- `stealthchop_threshold` is set to `999999` on X/Y/Z (always silent). Set to `0` on the extruder intentionally — stealthchop causes inconsistent extrusion on direct drive.
- Y motor current is slightly higher (0.9A vs 0.8A) to compensate for moving bed mass.
- `SAVE_CONFIG` will append calibration data below the marker at the bottom of `printer.cfg`. Do not edit that section manually.
