# Time limit of the cut-off phase LNS (Section 5.1)

`cutoff_time_limit.csv`: one row per instance (60 rows). The three-phase framework is run with a cut-off phase
LNS time limit of 5 s (the setting used in all other results), 30 s and 300 s; the pre-booking phase is the same.

| Column | Meaning |
|---|---|
| `instance_id`, `instance`, `seed` | Instance |
| `cutoff_objective_<T>` | Objective value of the cut-off schedule with time limit T (5s, 30s, 300s) |
| `cutoff_time_s_<T>` | Wall-clock time of the cut-off phase (s) |
| `final_pb_accepted_<T>`, `final_rt_accepted_<T>`, `final_objective_<T>` | Result after the real-time phase |
| `cutoff_objective_change_pct_<T>` | Change of the cut-off objective relative to 5 s (%; negative = improvement) |
| `commitment_windows_changed_<T>` | Number of CWs that differ from the 5 s run |
| `final_accepted_change_<T>`, `final_objective_change_<T>` | Change of the final accepted requests and objective value relative to 5 s |

## From the CSV to Section 5.1

- Cut-off objective improved = rows with `cutoff_objective_change_pct_<T>` < 0: 2 instances with 30 s and 4 with
  300 s, by at most 0.42%.
- Final result unchanged = rows with `final_accepted_change_<T>` = 0 and `final_objective_change_<T>` = 0: 58 with
  30 s and 56 with 300 s.
