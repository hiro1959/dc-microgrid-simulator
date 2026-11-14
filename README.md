# DC Microgrid Simulator (MATLAB/Simulink)

DOI: https://doi.org/10.5281/zenodo.21720183

**Current Version:** 3.1 (14 Nov. 2026)

---

## Related Publication

Yamada, H.; Liu, K.

*Autonomous Distributed Control of Residential Microgrids: A Simulation-Based Comparative Study.*

**Electronics** 2026, 15(20), 4786.

https://doi.org/10.3390/electronics15204786

---

## Overview

A MATLAB/Simulink-based simulator for analyzing and designing residential DC microgrids.

The simulator models:

- Photovoltaic (PV) generation
- Wind turbine generation
- LiFePO₄ batteries
- Battery-driven DC/DC converters
- Residential electrical loads
- Grid-interconnection systems

using simplified equivalent-circuit models suitable for long-term energy-flow simulation.

---

## Repository Contents

### Residential Microgrid Example Models

#### `Residential_grid_EL1R2.slx`

Autonomous distributed cooperative control model.

Features:

- PV + battery at each house
- Two wind turbines
- Utility-grid connection
- Battery-driven DC/DC converters
- SoC-based distributed coordination
- PV/wind output control based on neighboring battery SoC

#### `Residential_grid_EL2R2.slx`

Autonomous distributed control model.

Features:

- PV + battery at each house
- Two wind turbines
- Utility-grid connection
- Voltage-based distributed control
- Voltage-based grid power exchange
- PV/wind output curtailment based on bus voltage

### Device Models

- PV generation
- Wind turbine generation
- LiFePO₄ battery
- Battery-driven DC/DC converter
- Residential load
- Grid-interconnection unit

### Documentation

- English user manual
- Japanese user manual

### Data-Generation Scripts

- Python (PVLib)
- MATLAB

---

## Latest Update (Version 3.1)

Version 3.1 improves the interpolation scheme used for converting hourly weather and load data into one-second simulation inputs.

Major improvements:

- Replaced cubic-spline interpolation with Akima-spline interpolation.
- Eliminated overshoot and unrealistic negative values that could occur with cubic-spline interpolation.
- Improved interpolation accuracy for:
  - PV generation profiles
  - Wind-power generation profiles
  - Residential load profiles
- Added Appendix F describing interpolation methods and comparison results.
- Updated example models:
  - Residential_grid_EL1R2.slx
  - Residential_grid_EL2R2.slx
- Updated English and Japanese user manuals.

---

## Documentation

### English

`docs/DC_Grid_Simulator_User_Manual_Ver3.1.pdf`

### Japanese

`docs/DC_Grid_Simulator_User_Manual_Japanese_Ver3.1.pdf`

---

## Features

### PV Generation Model

- POA calculation using PVLib (Python)
- SAPM temperature model
- MPPT-based maximum-power operation
- Terminal-voltage-based output curtailment
- SoC-based output curtailment
- Dynamic Akima-spline interpolation of hourly weather data (Ver.3.1)

### Wind Turbine Model

- Cut-in / rated / cut-out wind-speed characteristics
- Terminal-voltage-based output curtailment
- SoC-based output curtailment
- Dynamic Akima-spline interpolation of hourly weather data (Ver.3.1)

### LiFePO₄ Battery Model

- Lookup-table voltage characteristics
- Internal resistance scaling
- SoC tracking
- Charge/discharge energy accumulation

### Battery-Driven DC/DC Converter

- Droop characteristics
- SoC monitoring
- Overcharge protection
- Overdischarge protection

### Residential Load Model

- Statistical monthly consumption model
- Random daily variation
- Typical hourly load pattern
- Dynamic Akima-spline interpolation of hourly load data (Ver.3.1)

### Grid-Interconnection Model

- Voltage-based power exchange
- SoC-based power exchange
- Constant-current import/export control

---

## Current Example Models (Recommended)

### Residential_grid_EL1R2.slx

Autonomous distributed cooperative control.

- SoC-based coordination among distributed energy resources
- SoC-based PV control
- SoC-based wind-power control
- SoC-based utility-grid power exchange

### Residential_grid_EL2R2.slx

Autonomous distributed control.

- Voltage-based control
- Voltage-based PV curtailment
- Voltage-based wind-power curtailment
- Voltage-based utility-grid power exchange

### Legacy Models

- `Residential_grid_EL1R.slx` (Ver.3.0)
- `Residential_grid_EL2R.slx` (Ver.3.0)
- `Residential_grid8.slx` (Ver.2.2)
- `Residential_grid9.slx` (Ver.2.2)

Retained for reference and reproducibility.

---

## Required Data Files

Before running the simulation, import the required MAT files into the MATLAB workspace.

### Solar Data (select the desired city)

- Solar_Sapporo2023_hourly.mat
- Solar_Sendai2023_hourly.mat
- Solar_Tokyo2023_hourly.mat
- Solar_Osaka2023_hourly.mat
- Solar_Fukuoka2023_hourly.mat
- Solar_Naha2023_hourly.mat

### Wind Data (select the desired city)

- Wind_Speed_Sapporo2023_hourly.mat
- Wind_Speed_Sendai2023_hourly.mat
- Wind_Speed_Tokyo2023_hourly.mat
- Wind_Speed_Osaka2023_hourly.mat
- Wind_Speed_Fukuoka2023_hourly.mat
- Wind_Speed_Naha2023_hourly.mat

### Residential Load Data

- House_load1.mat
- House_load2.mat
- House_load3.mat
- House_load4.mat
- House_load5.mat

### EV Charging Data

- EV_Charge_hourly.mat

Scripts for generating these files are provided in the `appendix/` folder.

---

## Data Files (Zenodo)

The MATLAB datasets required for simulation are hosted on Zenodo.

**Concept DOI (latest version):**

https://doi.org/10.5281/zenodo.21720183

The Zenodo archive contains:

### Solar Data

- Solar_Sapporo2023_hourly.mat
- Solar_Sendai2023_hourly.mat
- Solar_Tokyo2023_hourly.mat
- Solar_Osaka2023_hourly.mat
- Solar_Fukuoka2023_hourly.mat
- Solar_Naha2023_hourly.mat

### Wind Data

- Wind_Speed_Sapporo2023_hourly.mat
- Wind_Speed_Sendai2023_hourly.mat
- Wind_Speed_Tokyo2023_hourly.mat
- Wind_Speed_Osaka2023_hourly.mat
- Wind_Speed_Fukuoka2023_hourly.mat
- Wind_Speed_Naha2023_hourly.mat

### Residential Load Data

- House_load1.mat
- House_load2.mat
- House_load3.mat
- House_load4.mat
- House_load5.mat

### EV Charging Data

- EV_Charge_hourly.mat

---

## Running the Simulation

1. Open either:
   - `Residential_grid_EL1R2.slx`
   - `Residential_grid_EL2R2.slx`

2. Import the required MAT files into the MATLAB workspace.

3. Set the simulation stop time.

Example for one-year simulation:

```matlab
365*24*3600
```

4. Run the simulation.

5. Results including:

- Backbone voltage
- PV generation
- Wind generation
- Battery SoC
- Utility-grid power exchange
- Renewable-energy ratio
- Cumulative energy consumption

will be displayed through Simulink Scope and Display blocks.

---

## Version History

### Version 3.1 (2026-11-14)

Major changes:

- Replaced cubic-spline interpolation with Akima-spline interpolation for hourly-to-second data conversion.
- Improved PV, wind-power, and residential-load profile generation.
- Eliminated overshoot and unrealistic negative values caused by cubic-spline interpolation.
- Added Appendix F describing interpolation methods and comparison results.
- Added new example models:
  - Residential_grid_EL1R2.slx
  - Residential_grid_EL2R2.slx
- Updated English and Japanese user manuals:
  - DC_Grid_Simulator_User_Manual_Ver3.1.pdf
  - DC_Grid_Simulator_User_Manual_Japanese_Ver3.1.pdf

### Version 3.0 (2026-11-12)

Major changes:

- Replaced pre-interpolated 1-second datasets with original hourly datasets.
- Implemented dynamic cubic-spline interpolation during simulation.
- Reduced dataset size from hundreds of megabytes to several tens of kilobytes.
- Significantly reduced memory requirements.
- Added weather datasets for:
  - Sapporo
  - Tokyo
  - Osaka
  - Fukuoka
  - Naha
- Added new example models:
  - `Residential_grid_EL1R.slx`
  - `Residential_grid_EL2R.slx`
- Updated English and Japanese user manuals.

### Version 2.2 (2026-08-18)

- Improved PV and wind-turbine output curtailment based on DC backbone voltage.
- Added:
  - `Residential_grid8.slx`
  - `Residential_grid9.slx`
- Updated English and Japanese user manuals.