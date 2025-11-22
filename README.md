# Techno-Economic Optimization of PV, Battery & Electrolyzer System

## 📖 Project Overview
This project performs a techno-economic optimization of a hybrid Green Hydrogen production system consisting of **Solar PV**, a **Battery Energy Storage System (BESS)**, and an **Electrolyzer**.

The objective was to minimize the **Levelized Cost of Hydrogen (LCOH2)** while ensuring system stability and maximizing hydrogen production efficiency. The solution utilizes a custom energy management algorithm to size components optimally based on 1-year timeseries data.

## ⚙️ Methodology & Control Strategy
The core of this project is a Python-based optimization algorithm (using `scipy.optimize.minimize`) that determines the optimal component sizes. The system operates under a strict logic control strategy to manage energy flow:

### 1. Electrolyzer Operation
* **Nominal Operation:** The electrolyzer runs on direct solar power when $P_{pv} \ge 0.2 \cdot P_{e,nom}$ (20% minimum load threshold).
* **Battery Support:** If solar power is between $0.2 \cdot P_{e,nom}$ and the nominal capacity, it runs solely on PV. If solar drops below the 20% threshold, the **Battery (BESS)** discharges to bridge the gap, ensuring the electrolyzer stays online and avoiding shutdowns.

### 2. Battery Management (BESS)
* **Charging:** The battery charges only when there is surplus solar energy exceeding the electrolyzer's nominal power ($P_{pv} > P_{e,nom}$).
* **Protection Mode:** If combined Solar + Battery power is insufficient for hydrogen production, available solar energy is diverted to charge the battery. This prevents PV cell damage due to heating and prepares the battery for future cycles.
* **Constraints:**
    * Minimum SOC: 10%.
    * Modeled Lifetime: 20 years.

## 📊 Optimization Results
The algorithm simulated various configurations to find the "sweet spot" between system cost and production output.

| Parameter | Optimized Value |
| :--- | :--- |
| **Optimal PV Peak Power** | `2,150.31 kWp` |
| **Optimal Battery Capacity** | `180.72 kWh` |
| **Minimum LCOH2** | `6.56 €/kg` |
| **Annual H2 Production** | `30,640.77 kg` |

## 📈 Visualization

### Figure 1: System Performance Timeseries
<img width="756" height="578" alt="image" src="https://github.com/user-attachments/assets/3a05e86c-4f50-44a6-b188-36b018bd7f0a" />

> *The graph above illustrates the interplay between Solar generation, Battery SOC, and Hydrogen production over the course of the year.*

### Figure 2: LCOH2 Optimization Heatmap
<img width="747" height="377" alt="image" src="https://github.com/user-attachments/assets/8be23003-125f-4f4d-9253-79a67e17a78b" />

> *This contour graph highlights the regions of optimal cost (LCOH2) relative to variations in Solar PV size and Battery capacity.*
