# Table 4: three-phase framework versus fully fixed service

`fixed_service_vs_three_phase.csv`: one row per instance (60 rows).

| Column | Meaning |
|---|---|
| `instance_id`, `instance`, `seed`, `group` | Instance (`group` = `Leuven` or `random`) |
| `pb_requests`, `rt_requests` | Number of PB and RT requests |
| `fixed_services` | Number of scheduled services of the fully fixed service |
| `fixed_headway_min` | Headway between scheduled services (min; empty if only one service fits) |
| `fixed_served`, `fixed_served_pb`, `fixed_served_rt` | Requests served by the fully fixed service (total, PB, RT) |
| `fixed_dtd`, `fixed_ivt`, `fixed_objective` | Total DTD, total IVT (min) and objective value of the fully fixed service |
| `three_phase_accepted`, `three_phase_accepted_pb`, `three_phase_accepted_rt` | Requests accepted by the three-phase framework (total, PB, RT) |
| `three_phase_dtd`, `three_phase_ivt`, `three_phase_objective` | Total DTD, total IVT (min) and objective value of the three-phase framework |

## From the CSV to Table 4

Table 4 reports each group (30 rows) separately:

- Requests served (mean per instance) = mean of `fixed_served` or `three_phase_accepted`.
- Service rate (%) = sum of served requests / sum of (`pb_requests` + `rt_requests`) × 100; PB and RT rates likewise with the PB and RT columns.
- Service volume ratio = sum of `three_phase_accepted` / sum of `fixed_served`.
- Objective value = mean of `fixed_objective` or `three_phase_objective`; objective reduction = 1 − (SFPB mean / fixed mean).

Example: Leuven, fixed service 18.7 requests (17.0%), three-phase framework 59.7 requests (54.3%), ratio 3.2.
