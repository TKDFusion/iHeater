### iHeater Configuration for Klipper

This section contains configuration files for the iHeater chamber heater for 3D printers running the Klipper firmware. The configuration is designed to manage chamber heating and fans using the iHeater control board.

### Requirements

#### Hardware

* iHeater control board
* NTC 100K 3950 thermistors (2 pcs)
* PTC heating element 220V 100W, for the chamber
* 7530 220V fan, for air circulation inside the chamber
* Thermal fuse KSD9700 or similar (220V 5A 130°C)

#### Software

* Klipper (latest version)
* Configured and running Klipper host

### Klipper Configuration

Copy the `iHeater.cfg` configuration file into your `printer.cfg` directory(it could be /klipper_config) and include it using the `[include]` directive:

```bash
cd ~/klipper_config
```

```bash
wget https://raw.githubusercontent.com/pavluchenkor/iHeater/refs/heads/main/iHeater.cfg
```

### Connecting the iHeater MCU

Edit `iHeater.cfg` and specify the serial ID of your board:

```ini
[mcu iHeater]
serial: usb-Klipper_stm32f042x6_ХХХХХХХХХХХХХХХХХХХХХХХ-ХХХХ
```

## Preparation for Use

The configuration file includes the following section:

```ini
[gcode_macro CHAMBER_VARS]
variable_chamber_target: 0          # Target chamber temperature, °C
variable_start_offset: 10           # Chamber temperature sufficient for starting the print, °C
variable_delta_temp: 10             # Difference between chamber temperature and heater temperature, °C
variable_min_heater_temp: 50        # Minimum heater temperature (for cooling), °C
variable_max_heater_temp: 100       # Maximum heater temperature, °C
variable_control_interval: 1.0      # Control function call interval, seconds
variable_air_min_delta: 0.5         # Minimum difference between target and current chamber temperature (heater = target + delta_temp), °C
variable_air_max_delta: 5.0         # Maximum difference between target and current chamber temperature (heater = max_heater_temp), °C
gcode:
```

**The maximum allowable heater temperature depends on the enclosure material.**

To verify:

!. Set the heated bed to 95-100°C
1. Set the heater temperature to 100 °C using the Fluidd or Mainsail interface.
2. Ensure the iHeater is inside the printer's enclosed volume.
3. After reaching the set temperature, inspect areas where the heater contacts plastic parts of the enclosure. Plastic should not soften.
4. Increase the temperature by 5-10 °C and repeat the inspection.
5. Continue repeating this procedure until the maximum allowable heater temperature is identified without risking enclosure deformation.

This approach helps determine a safe maximum temperature and achieves optimal efficiency for the iHeater operation.


## Usage

### Chamber Heater Control Commands

* Setting the chamber temperature:

  ```
    M141 S60  ; Sets the chamber temperature to 60°C
  ```

* Waiting for the chamber to reach temperature:

  ```
    M191 S60  ; Waits until the chamber temperature reaches 60°C
  ```

* Turning off the chamber heater:

  ```
    iHEATER_OFF   ; Turns off the chamber heater
  ```

* At the end of your slicer's G-code, add `iHEATER_OFF` to correctly disable the chamber heating.

### Start G-code

Modern 3D slicers support the automatic activation of an active heated chamber during G-code generation for printing. To enable this, specify the chamber temperature in the filament properties. If the slicer lacks this functionality, you must manually add a command to enable chamber heating in the start G-code.

Procedure:

* Set the target chamber temperature.
* Activate bed heating to efficiently and quickly heat the chamber.
* Continue with the standard printing start G-code.

Example start G-code:

```
; --- Start of print start G-code ---

; ****** iHeater Start ******
M141 S60       ; Set chamber temperature to 60°C
; ****** iHeater End ******

; --- Remaining start G-code ---
; Activate bed heating
...
```

!!! warning "To ensure proper completion of the iHeater control macro, add the iHEATER_OFF command to the printer's end G-code."

```
; --- Start of print end G-code ---

; ****** iHeater Start ******
iHEATER_OFF
; ****** iHeater End ******

; --- Remaining end G-code ---
...
```


## Disable
To disable iHeater, you need to comment out the line [include iHeater.cfg] in the printer.cfg file:

```
# [include iHeater.cfg]
```
and remove the corresponding lines from the start and end G-code.


### Notes

* **Safety:**

  * Ensure all wiring is done properly and safely.
  * Verify that `min_temp` and `max_temp` values align with hardware specs.

* **Hardware Check:**

  * Test heater and fan functionality before use.
  * Monitor temperature during the initial runs.

* **PID Tuning:**

  * Perform PID calibration if precise temperature control is required.
