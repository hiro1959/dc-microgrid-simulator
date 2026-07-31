# DC Microgrid Simulator (MATLAB/Simulink)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21720183.svg)](https://doi.org/10.5281/zenodo.21720183)

A MATLAB/Simulink-based simulator for analyzing and designing DC microgrids in residential areas.  
The simulator models PV generation, wind turbines, batteries, DC/DC converters, household loads,  
and grid-interconnection behavior using simplified equivalent-circuit models.

This repository provides:
- Residential microgrid models (`Residential_grid1.slx`, `Residential_grid2.slx`)
- Device models (PV, wind turbine, LiFePO₄ battery, DC/DC converter, household load, grid-exchange unit)
- Weather-data processing scripts (Python + MATLAB)
- A complete 20-page user manual (PDF)

---

## Features

- **PV generation model**  
  - POA calculation using PVLib (Python)  
  - SAPM temperature model  
  - MPPT-like maximum power output  
  - Over-voltage output suppression

- **Wind turbine model**  
  - Cut-in / rated / cut-out wind-speed characteristics  
  - Output-limiting function based on bus voltage

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

### `Residential_grid1.slx`
- PV + battery at each house  
- Wind turbines at two bus locations  
- Grid connection at one end  
- Voltage-based grid power exchange  

### `Residential_grid2.slx`
- Battery-driven DC/DC converters  
- Grid connection at both ends  
- SOC-based grid power exchange  

---

## Data Files Required

Before running the simulation, import the following into MATLAB:

- `Solar_Sendai_2023.mat` — POA & temperature-correction data (1-second resolution)  
- `Wind_Speed.mat` — hourly wind-speed data  
- `House1(365).mat`–`House4(365).mat` — household load profiles (1-year, 365 days)
- `EV_Charge(Everyday_2AM~4AM_10kWh).mat` — daily EV charging load (2:00–4:00 AM daily)

Scripts for generating these files are provided in the `appendix/` folder.

## Data Files (Zenodo)

Large data files required for running the DC Microgrid Simulator are hosted on Zenodo.

**DOI: https://doi.org/10.5281/zenodo.21720183**

This dataset includes:
- Solar_Sendai_2023.mat (1.7 GB)
- House1(365).mat – House4(365).mat (200 MB each)
- Wind_Speed.mat
- EV_Charge(Everyday_2AM~4AM_10kWh).mat

All files are provided in MATLAB .mat format and are referenced by the Simulink model in this repository.

---

## Running the Simulation

1. Open the desired Simulink model (`Residential_grid1.slx` or `Residential_grid2.slx`)
2. Import all required `.mat` files into the MATLAB workspace
3. Set simulation end time (e.g., one year = `365*24*3600`)
4. Run the simulation  
5. Results (bus voltage, PV/wind output, grid exchange, battery SOC, cumulative energy)  
   will appear in Scope and Display blocks

---

## Directory Structure (recommended)

dc-microgrid-simulator/
│
├─ README.md
├─ LICENSE
├─ docs/
│   └─ DC_Microgrid_Manual.pdf
│
├─ models/
│   ├─ Residential_grid1.slx
│   └─ Residential_grid2.slx
│
├─ data/
│   ├─ Solar_Sendai_2023.mat
│   ├─ Wind_Speed.mat
│   ├─ House1(365).mat
│   ├─ House2(365).mat
│   ├─ House3(365).mat
│   ├─ House4(365).mat
│   └─ EV_Charge(Everyday_2AM~4AM_10kWh).mat
│
├─ scripts/
│   ├─ python/
│   │   └─ GHI_to_POA.py
│   └─ matlab/
│       ├─ POA_SAPM_to_1sec.m
│       └─ generate_load_profiles.m

