# Urban-Runoff-Pollutant-Model

Object-oriented hydrological and water quality model for simulating **urban runoff** and **pollutant loads** at the sub-basin scale.

This project was originally developed as part of a graduate course on **Hydrological Models** and has since been refactored into a clean, reusable Python package suitable for research, teaching, and model demonstration.

---

## 🌧️ What does this model do?

Given:

- a **rainfall event** (daily precipitation),
- the **land-use / soil group** of each sub-basin,
- **crop coefficients (k_c)**,
- and **pollutant concentrations** per land-use class,

the model:

1. Computes **area-weighted Curve Number (CN)** and **k_c** for the entire catchment.
2. Applies the **SCS–CN method** to estimate:
   - potential maximum retention **S [mm]**
   - initial abstraction **I<sub>a</sub> [mm]**
   - daily evapotranspiration **ET<sub>daily</sub> [mm]**
   - effective rainfall (runoff depth) **P<sub>e</sub> [mm]**
   - infiltration **F [mm]**
3. For each **sub-basin**, it computes:
   - runoff depth **P<sub>e</sub> [mm]**
   - runoff volume **[m³]** and **[L]**
   - infiltration **F [mm]**
4. Multiplies runoff volume (L) by pollutant concentrations to obtain:
   - **TN load [mg]**
   - **TP load [mg]**
   - **BOD load [mg]**
   - **TSS load [mg]**
5. Stores all results (runoff + pollutants) in a structured **JSON output file**.

---

## 📂 Project structure

A suggested repo layout:

```text
Urban-Runoff-Pollutant-Model/
│
├── urban_runoff_model.py        # main Python script (this repository's core)
├── README.md                    # this file
├── requirements.txt             # Python dependencies (json, etc. + optional)
│
├── data/                        # input data (JSON format)
│   ├── scenario1.json           # exam / case study 1
│   ├── scenario2.json           # exam / case study 2 (optional)
│   ├── landuse_soilgroup.json   # land use & hydrologic soil group properties
│   └── pollutants.json          # pollutant concentrations per LU_Code
│
└── outputs/
    └── output_results_scenario1.json   # example model output (created at runtime)
