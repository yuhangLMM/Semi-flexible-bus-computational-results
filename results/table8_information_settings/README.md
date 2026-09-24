# Table 8: information settings and decomposition of the acceptance gap

`information_settings.csv`: one row per instance (60 rows), accepted requests (PB + RT) under four settings.

| Column | Meaning |
|---|---|
| `instance_id`, `instance`, `seed` | Instance |
| `requests` | Number of requests (PB + RT) |
| `three_phase_accepted` | Three-phase framework |
| `pb_all_known_accepted` | PB all known: all PB requests decided together at the cut-off, then as the three-phase framework |
| `rt_all_known_accepted` | RT all known: PB decisions and CWs of the three-phase framework, all RT requests known at the start of operations |
| `full_information_accepted` | Deterministic full-information reference (all PB and RT requests known in advance) |
| `full_information_accepted_pb`, `full_information_accepted_rt` | PB and RT part of the reference |
| `gap_pb` | `pb_all_known_accepted` − `three_phase_accepted` |
| `gap_rt` | `rt_all_known_accepted` − `three_phase_accepted` |
| `gap_commitment` | `gap_total` − `gap_pb` − `gap_rt` (early commitment of PB requests) |
| `gap_total` | `full_information_accepted` − `three_phase_accepted` |

The deterministic full-information reference is computed with the LNS (15 parallel workers, each stopping after
60 s without improvement, at most 600 s), starting from an empty schedule.

## From the CSV to Table 8

Each table row = mean over the three seeds of the instance; the average row = mean over all 60 rows
(63.8 / 68.6 / 65.5 / 79.3 accepted requests; gap parts 4.8 / 1.7 / 9.0 / 15.5). `gap_commitment` is positive in
all 60 instances.
