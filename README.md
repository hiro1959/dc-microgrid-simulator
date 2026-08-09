# DC Microgrid Simulator (MATLAB/Simulink)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21720183.svg)](https://doi.org/10.5281/zenodo.21720183)

A MATLAB/Simulink-based simulator for analyzing and designing DC microgrids in residential areas.  
The simulator models PV generation, wind turbines, batteries, DC/DC converters, household loads,  
and grid-interconnection behavior using simplified equivalent-circuit models.

This repository provides:
- Residential microgrid models (`Residential_grid5.slx`, `Residential_grid7.slx`)
- Device models (PV, wind turbine, LiFePO₄ battery, DC/DC converter, household load, grid-exchange unit)
- Weather-data processing scripts (Python + MATLAB)
- User manuals (English & Japanese)

---

## Documentation

- **DC Grid Simulator User Manual (English)**  
  `docs/DC_Grid_Simulator_User_Manual.pdf`

- **DC Grid Simulator User Manual (Japanese)**  
  `docs/DC_Grid_Simulator_User_Manual_Japanese.pdf`

---

## Features

- **PV generation model**  
  - POA calculation using PVLib (Python)  
  - SAPM temperature model  
  - MPPT-like maximum power output  
  - Over-voltage output suppression
  - Over-charging output suppression

- **Wind turbine model**  
  - Cut-in / rated / cut-out wind-speed characteristics  
  - Output-limiting function based on bus voltage
  - Over-charging output suppression

- **LiFePO₄ battery model**  
  - Lookup-table voltage characteristics  
  - Internal resistance scaling  
  - SOC tracking  
  - Charge/discharge cumulative energy & current

- **Battery-driven DC/DC converter**  
  - Droop characteristics  
  - SOC-based grid power exchange  
  - Overcharge/overdischarge protection

- **Household load model**  
  - Statistical monthly consumption  
  - Random daily variation  
  - Typical hourly load profile  
  - 1-second resolution load data generation

- **Grid-interconnection model**  
  - Voltage-based or SOC-based power exchange  
  - Constant-current import/export control

---

## Microgrid Models Included

### `Residential_grid5.slx`
- PV + battery at each house  
- Wind turbines at two bus locations  
- Grid connection at one point  
- Voltage-based grid power exchange  

### `Residential_grid7.slx`
- Battery-driven DC/DC converters  
- Grid connection at one point  
- SOC-based grid power exchange  
- PV/wind generation control based on nearest battery SoC

---

## Data Files Required

Before running the simulation, import the following into MATLAB:

- `Solar_Sendai_2023.mat` — POA & temperature-correction data (1-second resolution)  
- `Wind_Speed_Sendai_2023.mat` — hourly wind-speed data  
- `House1.mat`–`House5.mat` — household load profiles (1-year, 365 days)  
- `EV_Charge.mat` — daily EV charging load (2:00–4:00 AM)

Scripts for generating these files are provided in the `appendix/` folder.

---

## Data Files (Zenodo)

Large data files required for running the DC Microgrid Simulator are hosted on Zenodo.

**DOI: https://doi.org/10.5281/zenodo.21720183**

This dataset includes:
- Solar_Sendai_2023.mat  
- Wind_Speed_Sendai_2023.mat  
- House1.mat – House5.mat  
- EV_Charge.mat  

All files are provided in MATLAB .mat format and are referenced by the Simulink models in this repository.

---

## Running the Simulation

1. Open the desired Simulink model (`Residential_grid5.slx` or `Residential_grid7.slx`)
2. Import all required `.mat` files into the MATLAB workspace
3. Set simulation end time (e.g., one year = `365*24*3600`)
4. Run the simulation  
5. Results (bus voltage, PV/wind output, grid exchange, battery SOC, cumulative energy)  
   will appear in Scope and Display blocks
