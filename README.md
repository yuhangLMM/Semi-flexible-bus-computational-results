# Semi-DRT Computational Results

This repository contains the instances and computational results used for Tables 5-8 of the semi-DRT study.

## Contents

- `instances/`  
  Input instances used in the computational experiments.
  - `leuven_real_network/`: Leuven real-network instances, `leuven-01` to `leuven-10`.
  - `random_network/`: random-network instances, `rand-01` to `rand-10`.

- `table5_prebooking/`  
  Results for the online pre-booking acceptance phase.
  - `gurobi/`: Gurobi benchmark results.
  - `lns/`: LNS results.

- `table6_reoptimization/`  
  Results for the offline booking cut-off re-optimization phase.
  - `gurobi/`: Gurobi benchmark results.
  - `lns/`: LNS results.

- `table7_realtime_control/`  
  Results for day-of-operations real-time control.
  - `full_rolling_milp/`: full rolling MILP reference results.
  - `compressed_rolling_milp/`: compressed rolling MILP results.

- `table8_static_reference/`  
  Static full-information LNS reference results.

## Files

Each instance folder contains the corresponding summary files and, where available, detailed passenger, stop, arc, timing, or state outputs.

`manifest.csv` records the original source path and the renamed destination path for each copied file.

Instance names follow the paper notation: `leuven-01` to `leuven-10` and `rand-01` to `rand-10`.
