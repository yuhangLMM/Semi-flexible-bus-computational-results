# Semi-flexible bus computational results

Instances, detailed solutions, and computational results for the paper

> **Commitment-Aware Online Operations for Semi-Flexible Public Bus Services with Pre-Booked and Real-Time Requests**
> Yuhang Wu, Dilay Aktas, Pieter Vansteenwegen (KU Leuven Institute for Mobility – MIM)

This version contains the results of the **revised manuscript (r1 revision)**.
The results of the first submission are kept unchanged under the tag
[`r1-submission`](https://github.com/yuhangLMM/Semi-flexible-bus-computational-results/tree/r1-submission).

## Instances and seeds

The experiments use 20 instances: ten on the real Leuven network (`leuven-01` to `leuven-10`) and ten on
random networks (`rand-01` to `rand-10`). Their settings are listed in Table 2 of the paper. For each instance,
the requests are generated with three random seeds, which gives 60 instances in total. They are named
`<instance>_s<seed>`, for example `leuven-01_s1`. Most tables in the paper report, for each of the 20 instances,
the mean over its three seeds.

| Instance | Group | PTW width (min) | PB / RT requests | Vehicles | Stops | Service period |
|---|---|---:|---:|---:|---:|---|
| leuven-01 | Leuven | 10 | 50 / 50 | 4 | 50 | 06:00–09:00 |
| leuven-02 | Leuven | 10 | 50 / 50 | 5 | 50 | 06:00–09:00 |
| leuven-03 | Leuven | 20 | 50 / 50 | 4 | 50 | 06:00–09:00 |
| leuven-04 | Leuven | 6 | 50 / 50 | 4 | 50 | 06:00–09:00 |
| leuven-05 | Leuven | 10 | 50 / 50 | 3 | 50 | 06:00–09:00 |
| leuven-06 | Leuven | 10 | 30 / 70 | 4 | 50 | 06:00–09:00 |
| leuven-07 | Leuven | 10 | 70 / 30 | 4 | 50 | 06:00–09:00 |
| leuven-08 | Leuven | 10 | 100 / 100 | 4 | 50 | 06:00–09:00 |
| leuven-09 | Leuven | 10 | 50 / 50 | 4 | 50 | 06:00–09:00 |
| leuven-10 | Leuven | 10 | 50 / 50 | 4 | 50 | 06:00–09:00 |
| rand-01 | random | 10 | 40 / 40 | 3 | 40 | 06:00–08:00 |
| rand-02 | random | 10 | 50 / 50 | 4 | 50 | 06:00–09:00 |
| rand-03 | random | 10 | 60 / 60 | 5 | 60 | 06:00–10:00 |
| rand-04 | random | 10 | 30 / 30 | 4 | 30 | 06:00–11:00 |
| rand-05 | random | 10 | 50 / 50 | 4 | 50 | 06:00–09:00 |
| rand-06 | random | 20 | 40 / 40 | 3 | 40 | 06:00–08:00 |
| rand-07 | random | 20 | 50 / 50 | 4 | 50 | 06:00–09:00 |
| rand-08 | random | 20 | 60 / 60 | 5 | 60 | 06:00–10:00 |
| rand-09 | random | 20 | 30 / 30 | 4 | 30 | 06:00–11:00 |
| rand-10 | random | 20 | 50 / 50 | 4 | 50 | 06:00–09:00 |

`instances/instance_mapping.csv` maps each public name to the internal file name used during the experiments
(internal labels `original`, `seed_101` and `seed_202` correspond to seeds 1, 2 and 3) and gives the SHA-256
hash of every instance file.

## Abbreviations and method names

| Term | Meaning |
|---|---|
| PB | pre-booked request |
| RT | real-time request |
| PTW | pickup time window (given to the passenger when the request is accepted) |
| CW | commitment window: a window inside the PTW, half as wide, that the pickup must respect; issued to the accepted PB requests at the booking cut-off and to each RT request when it is accepted |
| DTD | departure time deviation (min) |
| IVT | in-vehicle time (min) |
| three-phase framework | the proposed method: pre-booking phase (LNS), booking cut-off phase (LNS), real-time phase (compressed real-time MILP) |
| fully fixed service | the same fleet on a fixed timetable that stops at every stop |
| full real-time MILP | the real-time MILP without the search-space restrictions (reference for the real-time phase) |
| PB all known | all PB requests are known at the cut-off and decided together; the rest as in the three-phase framework |
| RT all known | PB decisions and CWs as in the three-phase framework; all RT requests are known at the start of operations |
| deterministic full-information reference | all PB and RT requests are known in advance and decided together |
| buffer policy (10/20/30%) | PB admission policy that keeps a buffer of 10, 20 or 30% of the PTW width at both window ends |
| two-pool policy | PB admission policy that evaluates each PB request with sampled future RT requests |

Objective value = 1000 × (number of rejected requests) + total DTD + total IVT. All schedule times are in minutes
after midnight of the service day (360 = 06:00). Computation times are in seconds.

## Repository layout

| Folder | Content | Paper |
|---|---|---|
| `instances/` | The 60 instance files (network, travel times, fleet, requests with submission times) | Table 2, Section 5.1 |
| `solutions/` | Detailed three-phase framework solution of every instance: pre-booking decisions, cut-off schedule with CWs, final schedule | Section 5.2.1, Figs. 6–7 |
| `results/table4_fixed_service/` | Three-phase framework versus fully fixed service | Table 4 |
| `results/table5_6_lns_vs_gurobi/` | LNS versus Gurobi in the pre-booking and cut-off phases | Tables 5 and 6 |
| `results/table7_realtime_milp/` | Compressed versus full real-time MILP | Table 7 |
| `results/table8_information_settings/` | Four information settings and the decomposition of the acceptance gap | Table 8 |
| `results/fig9_admission_policies/` | Buffer policy and two-pool policy versus the three-phase framework | Fig. 9, Section 5.4.2 |
| `results/fig10_sensitivity/` | Accepted requests per instance for the sensitivity analysis | Fig. 10, Section 5.5 |
| `results/cutoff_time_limit/` | Cut-off phase LNS with time limits of 5, 30 and 300 s | Section 5.1 |

Every results folder has one CSV file with one row per instance (60 rows, or 240 rows for the four admission
policies) and a short README that explains the columns and how the numbers in the paper are obtained from them.

## Notes

- Gurobi and the full real-time MILP results of the ten Leuven seed-1 instances (`leuven-01_s1` to
  `leuven-10_s1`) are the results of the first submission; their raw outputs are in the tag `r1-submission`.
  All other results were computed for the revision.
- Solve times depend on the hardware; the LNS results depend on the random seed of the search and on the
  time limits.
