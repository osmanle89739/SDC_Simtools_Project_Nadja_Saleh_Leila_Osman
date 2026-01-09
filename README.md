# Hospital Bed Occupancy Simulation (COVID-19 Nuremberg)

This project simulates occupancy levels and waiting times in hospitals (intensive care units and general wards) in Nuremberg using **Discrete Event Simulation (DES)**. The objective is to analyze the impact of varying patient volumes on waiting times and system stability.

## Overview

The simulation utilizes the simpy library to model the processes of patient admission, length of stay (LOS), and resource scarcity (bed capacity). Two scenarios are compared: standard operations and a stress test under high-load conditions.

### Core Features

* **Monte Carlo Simulation:** Execution of independent replications for uncertainty quantification.
* **Warm-up Phase:** Pre-occupancy of beds (75% initial capacity) to achieve a realistic steady state and minimize initialization bias.
* **Stochastic Processes:** Modeling of arrivals and treatment durations using exponential distributions.
* **Statistical Evaluation:** Calculation of mean values, standard errors, confidence intervals, and 95th percentiles of waiting times.

---

## Project Structure

```text
project/
├── notebooks/
│   └── MonteCarlosimulationFInal.ipynb  # Main analysis and final results
├── src/
│   └── simulation_logic.py              # Core logic of the DES (SimPy) and MC loops
├── tests/
│   └── infunferschrittern.ipynb         # Extended scenarios (5-unit steps) for tipping point analysis
├── requirements.txt                     # List of dependencies
└── README.md                            # Project description

```

---

## Technologies

* **Python 3.x**
* **SimPy:** Framework for event-oriented simulation.
* **NumPy:** Mathematical calculations and random number generation.
* **Pandas:** Data structuring and tabular representation of results.

---

## Parameters and Configuration

The capacities are based on real-world data for the Nuremberg location:

| Parameter | Value | Description |
| --- | --- | --- |
| ICU_BEDS | 51 | Available intensive care beds |
| NORM_BEDS | 567 | Available general ward beds |
| MEAN_LOS | 14.0 days | Mean Length of Stay |
| SIM_DURATION | 150 days | Total simulation period |
| R | 20 | Number of simulation runs (replications) |

---

## Simulation Execution

### Model Functionality

1. **Initialization:** The hospital is populated to 75% capacity with "preload" patients to minimize transient effects.
2. **Arrival Process:** Patients arrive based on a Poisson process (exponential distribution of inter-arrival times).
3. **Treatment:** If a bed is available, it is occupied. Treatment duration is stochastic. If no bed is available, a waiting period occurs.
4. **Evaluation:** After 150 days, statistics for the respective replication scenarios are aggregated.

### Starting the Simulation

Ensure all dependencies are installed:

```bash
pip install simpy numpy pandas

```

Execute the script:

```bash
python simulation_script.py

```

---

## Results and Scenario Comparison

The model compares two primary scenarios:

1. **Normal (35 patients/week):** Represents regular operations.
2. **Stress Test (235 patients/week):** Tests the system at its theoretical capacity limit.

The results are presented in a table comparing the theoretical utilization (rho) against mean waiting times and the corresponding confidence intervals.