# EMS Station Placement — Minimax (p-center style) MILP in PuLP

This repository contains my semestral project for **Czech Technical University in Prague (CTU), Faculty of Transportation Sciences**.

## Problem
We consider a set of city districts. In each district there is a candidate location for building an Emergency Medical Service (EMS) station.

Goal: **minimize the maximum (worst-case) travel time** while respecting:
- **Budget constraint** (total build cost ≤ 50 million)
- **Logical constraint**: if a station is built in district 2, then district 6 must not have a station
- Each district must be served by exactly one built station

The model is formulated as a **mixed-integer linear program (MILP)** and solved using **PuLP**.

## Notebooks
This repository contains **two notebooks** with the same problem solved using **slightly different approaches**:

- **Version 1** (`ems_station_minimax_teacher_version_1.ipynb`) — teacher-style formulation (reads inputs from `Data.xlsx`).
- **Version 2** (`ems_station_minimax_version_2.ipynb`) — my formulation with clearer structure/markdown and loop-based variables/constraints.

## Model (short)
Decision variables:
- `y[i]` — build station in district `i` (binary)
- `x[i,j]` — district `j` is served by station `i` (binary)
- `h` — maximum travel time (continuous)

Objective:
- minimize `h`

Main constraints:
- `d[i][j] * x[i,j] <= h` for all `i, j`
- `x[i,j] <= y[i]` for all `i, j`
- `sum_i x[i,j] == 1` for all `j`
- budget and mutual-exclusion rule

## Files
- `ems_station_minimax.ipynb` — notebook with explanation + implementation + results

## How to run
1. Clone the repository
2. Install requirements:
   ```bash
   pip install pulp pandas
