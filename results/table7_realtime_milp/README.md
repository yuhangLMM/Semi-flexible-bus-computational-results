# Table 7: compressed real-time MILP versus full real-time MILP

`compressed_vs_full_realtime_milp.csv`: one row per instance (60 rows). Both models start from the same cut-off
schedule and CWs of the three-phase framework and process the same RT requests one by one (one epoch per request
arrival).

| Column | Meaning |
|---|---|
| `instance_id`, `instance`, `seed` | Instance |
| `pb_accepted`, `pb_rejected` | PB requests accepted and rejected before the real-time phase |
| `rt_requests` | Number of RT requests |
| `full_status` | `completed`, or `time_limit` if the full real-time MILP did not finish within three hours (rand-08, all seeds) |
| `full_result_source` | `r1` = result of the first submission (Leuven seed 1), `revision` = computed for the revision |
| `full_rt_accepted`, `full_rt_rejected` | RT requests accepted and rejected by the full real-time MILP |
| `full_solver_time_s` | Solver time summed over all epochs (s) |
| `full_wall_time_s` | Wall-clock time of the whole real-time phase (s) |
| `full_max_epoch_s`, `full_avg_epoch_s`, `full_epochs` | Longest and average solver time per epoch (s), number of epochs |
| `full_total_accepted`, `full_objective` | Accepted requests (PB + RT) and objective value at the end of the day |
| `compressed_*` | Same quantities for the compressed real-time MILP of the three-phase framework |

Columns of the full real-time MILP are empty when `full_status = time_limit`.

## From the CSV to Table 7

- Each table row is one instance: mean over the three seeds of `pb_accepted`/`pb_rejected`, RT Acc/Rej, Time (s)
  (`*_solver_time_s`), Max Ep. (`*_max_epoch_s`), Avg Ep. (`*_avg_epoch_s`) and Total Acc/Rej.
- The average row excludes rand-08.
- Totals over the 57 instances where the full real-time MILP completes: 1313 RT requests accepted by the compressed
  and 1319 by the full real-time MILP; the longest compressed epoch over all 60 instances is 0.477 s.
