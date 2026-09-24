# Detailed solutions of the three-phase framework

One folder per instance: `leuven/<instance_id>/` and `random/<instance_id>/` (60 folders). Times are in minutes
after midnight of the service day (360 = 06:00); computation times are in seconds. Vehicle trips are identified
by `vehicle` and `trip`.

| File | Content |
|---|---|
| `phase1_prebooking_decisions.csv` | Pre-booking phase: every PB request in submission order with the immediate decision (`accepted` / `rejected`) |
| `phase2_cutoff_requests.csv` | Booking cut-off phase: every PB request with its assigned vehicle trip, planned pickup and drop-off, and the CW issued at the cut-off (rejected requests have empty fields) |
| `phase2_cutoff_timetable.csv` | Cut-off schedule: stops visited by each vehicle trip with arrival and departure times |
| `phase3_final_requests.csv` | Real-time phase: every PB and RT request with its final status, vehicle trip, pickup, drop-off, CW, DTD and IVT |
| `phase3_final_timetable.csv` | Final schedule after the real-time phase: stops visited by each vehicle trip |
| `summary.json` | Accepted requests, objective values and computation times of the three phases, number of vehicle trips used, and the number of CW violations |

## Columns

| Column | Meaning |
|---|---|
| `order` | Position of the PB request in the submission sequence |
| `request_id` | Request id as in the instance file |
| `type` | `PB` or `RT` |
| `request_time` | Submission time (min; negative = submitted on an earlier day) |
| `origin`, `destination` | Pickup and drop-off stop |
| `desired_time` | Desired departure time (min) |
| `ptw_lb`, `ptw_ub` | PTW (min) |
| `decision`, `status` | `accepted` or `rejected` |
| `vehicle`, `trip` | Serving vehicle trip |
| `pickup`, `dropoff` | Pickup and drop-off time (min) |
| `cw_lb`, `cw_ub` | CW (min). For PB requests it is issued at the cut-off and is identical in phase 2 and phase 3 |
| `dtd`, `ivt` | Departure time deviation and in-vehicle time (min) |
| `stop`, `arrival`, `departure` | Stop visited by the vehicle trip and its arrival and departure time (min) |
| `stop_type` | `mandatory` or `optional` stop |

`three_phase_summary.csv` collects the `summary.json` files of all 60 instances. Its main columns: `phase1_*`
(pre-booking phase), `phase2_*` (cut-off phase), `pb_accepted`, `rt_accepted`, `total_accepted`, `objective`,
`total_dtd`, `total_ivt` (final result), `phase3_solver_time_s` (solver time summed over the real-time epochs),
`phase3_wall_time_s`, `phase3_epochs`, `phase3_max_epoch_s`, `phase3_avg_epoch_s`, `vehicle_trips_used`, and
`cw_violations` (accepted requests whose final pickup lies outside their CW; 0 in all 60 instances).

Example (Section 5.2.1, Figs. 6–7): `leuven/leuven-01_s1/` accepts 64 requests (38 PB + 26 RT) with 7 vehicle trips.

## Raw outputs

`raw_outputs_leuven.zip` and `raw_outputs_random.zip` contain the original output files of the three phases for
each instance (`phase1/`, `phase2/`, `phase3/`), from which the CSV files above were derived:

- `*_final_summary.json`: pre-booking phase summary (accepted and rejected PB ids, objective, time per epoch, schedule);
- `*_reopt_summary.json`, `*_MM2_baseline.json` in `phase2/`: cut-off schedule and CWs (`tw_narrow_lb`, `tw_narrow_ub`; `tw_lb`, `tw_ub` = PTW; `d_pick0`, `a_drop0` = planned pickup and drop-off);
- `*_rolling_summary.json`, `*_MM2_baseline.json`, `*_passengers_detail.csv`, `*_stops_detail.csv`, `*_epoch_timing.csv` in `phase3/`: real-time phase result, final schedule and per-epoch solve times.
