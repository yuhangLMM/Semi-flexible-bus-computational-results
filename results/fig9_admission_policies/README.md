# Fig. 9: PB admission policies

`admission_policies.csv`: one row per policy and instance (4 policies × 60 instances = 240 rows). Each policy
changes only the pre-booking phase; the cut-off and real-time phases are those of the three-phase framework.

| Column | Meaning |
|---|---|
| `policy` | `buffer_10`, `buffer_20`, `buffer_30` (buffer policy with 10, 20, 30% of the PTW width) or `two_pool` (two-pool policy) |
| `instance_id`, `instance`, `seed` | Instance |
| `three_phase_pb_accepted`, `three_phase_rt_accepted`, `three_phase_total_accepted`, `three_phase_objective` | Result of the three-phase framework |
| `policy_pb_accepted`, `policy_rt_accepted`, `policy_total_accepted`, `policy_objective` | Result with the admission policy |
| `proactive_rejections` | Feasible PB requests rejected by the policy |
| `change_pb_accepted`, `change_rt_accepted`, `change_total_accepted`, `change_objective` | Policy − three-phase framework (negative `change_objective` = improvement) |

## From the CSV to Fig. 9 and Section 5.4.2

- Each marker in Fig. 9 is one row (`change_pb_accepted`, `change_rt_accepted`); group means are taken over the 30
  Leuven or 30 random-network rows of a policy.
- Mean `proactive_rejections` per policy: 3.2 (`buffer_10`) to 8.3 (`two_pool`).
- Objective better / equal / worse than the three-phase framework = count of `change_objective` < 0 / = 0 / > 0:
  28/2/30 for `buffer_30` and 28/1/31 for `two_pool`.
- Relative change of the total objective = sum of `change_objective` / sum of `three_phase_objective`.
