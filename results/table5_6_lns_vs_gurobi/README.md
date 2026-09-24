# Tables 5 and 6: LNS versus Gurobi in the pre-booking and cut-off phases

- `prebooking_phase_lns_vs_gurobi.csv`: pre-booking phase (Table 5), one row per instance (60 rows).
- `cutoff_phase_lns_vs_gurobi.csv`: booking cut-off phase (Table 6), one row per instance (60 rows). Each method
  starts from its own pre-booking result, so the accepted/rejected counts are those of the pre-booking phase.

| Column | Meaning |
|---|---|
| `instance_id`, `instance`, `seed` | Instance |
| `gurobi_status` | `optimal` = Gurobi proved every epoch optimal; `time_limit` = Gurobi could not prove all epochs of the pre-booking phase optimal within the time limit (three hours per instance; a run was stopped early when one epoch was not proven optimal within 30 min); `not_run` = cut-off phase not solved because the Gurobi pre-booking phase has no result |
| `gurobi_result_source` | `r1` = result of the first submission (Leuven seed 1), `revision` = computed for the revision |
| `gurobi_accepted`, `gurobi_rejected` | PB requests accepted and rejected by Gurobi |
| `gurobi_dtd`, `gurobi_ivt`, `gurobi_objective` | Total DTD, total IVT (min) and objective value of the Gurobi solution |
| `gurobi_time_s` | Gurobi computation time (s): whole pre-booking phase (Table 5) or the cut-off solve (Table 6) |
| `lns_accepted`, `lns_rejected`, `lns_dtd`, `lns_ivt`, `lns_objective`, `lns_time_s` | Same quantities for the LNS |
| `obj_gap_pct` | (LNS objective − Gurobi objective) / Gurobi objective × 100, only where Gurobi is optimal; negative = LNS lower |

Gurobi columns are empty when `gurobi_status` is not `optimal`.

## From the CSV to Tables 5 and 6

- Each table row is one instance. LNS columns = mean over the three seeds. Gurobi columns = mean over the seeds with
  `gurobi_status = optimal` (marked † in the paper when this is only one or two seeds; N/A or TL when none).
- Obj.Gap (%) of a row = mean of |`obj_gap_pct`| over the seeds with a Gurobi result; * marks rows where the LNS
  objective is lower on average.
- Average row: mean of the instance rows over the 17 instances with at least one optimal Gurobi result (the same
  17 instances for LNS). The average Obj.Gap is taken over the 39 seeds of the 13 instances where Gurobi is optimal
  for all three seeds.

Examples: Gurobi is optimal for 44 of the 60 instances; on these, LNS accepts the same number of requests in 40 and
more in 4. Average pre-booking time over the 17 instances: Gurobi 1574.4 s, LNS 121.1 s; cut-off phase: 146.4 s and 5.9 s.
