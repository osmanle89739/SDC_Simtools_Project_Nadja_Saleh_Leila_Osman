# Hospital Bed Occupancy Simulation (COVID-19 Nuremberg)

This project simulates the occupancy levels and waiting times in hospitals (intensive care units and general wards) in Nuremberg using **Discrete Event Simulation (DES)**. The objective is to analyze the impact of varying patient volumes on waiting times and system stability.

## Overview

The simulation utilizes the simpy library to map the processes of patient admission, length of stay (LOS), and resource scarcity (bed capacity). Two scenarios are compared: standard operations and a stress test under high-load conditions.

### Core Features:

* **Monte Carlo Simulation:** Execution of independent replications for uncertainty quantification.
* **Warm-up Phase:** Pre-occupancy of beds (75% initial capacity) to achieve a realistic steady state.
* **Stochastic Processes:** Modeling of arrivals and treatment durations using exponential distributions.
* **Statistical Evaluation:** Calculation of mean values, standard errors, confidence intervals, and 95th percentiles of waiting times.

---

### Project Structure

project/
├── notebooks/
│   └── MonteCarlosimulationFInal.ipynb  # Main analysis and final results
├── src/
│   └── simulation_logic.py              # Core logic of the DES (SimPy) and MC loops
├── tests/
│   └── infunferschrittern.ipynb         # Extended scenarios (steps of 5) for tipping point identification
├── requirements.txt                     # Required Python libraries
└── README.md                            # Project description

---

## Technologies

* **Python 3.x**
* **SimPy:** Framework for discrete-event simulation.
* **NumPy:** Mathematical calculations and random number generation.
* **Pandas:** Data structuring and tabular representation of results.

---

## Parameters & Configuration

Capacities are based on real-world data for the Nuremberg location:

| Parameter | Value | Description |
| --- | --- | --- |
| `ICU_BEDS` | 47 | Available intensive care beds |
| `NORM_BEDS` | 400 | Available general ward beds |
| `MEAN_LOS` | 14.0 days | Mean Length of Stay |
| `SIM_DURATION` | 150 days | Total simulation period |
| `R` | 20 | Number of simulation runs (replications) |

---

## Simulation Execution

### Model Functionality

1. **Initialization:** The hospital is populated to 75% capacity with "preload" patients to minimize transient effects.
2. **Arrival Process:** Patients arrive based on a Poisson process (exponential distribution of inter-arrival times).
3. **Treatment:** If a bed is available, it is occupied. Treatment duration is stochastic. If no bed is available, a waiting period occurs.
4. **Evaluation:** After 150 days, statistics for the respective replication scenario are aggregated.

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

## Results (Scenario Comparison)

The model compares two main scenarios:

1. **Normal (35 patients/week):** Represents regular operations.
2. **Stress Test (235 patients/week):** Tests the system at its theoretical capacity limit.

The results are output in a table comparing the **theoretical utilization ()** with the mean **waiting time** and the **confidence interval**.

