# Fig. 10: sensitivity to supply, demand, and service design

`sensitivity.csv`: one row per instance (60 rows). Fig. 10 uses the Leuven rows; the random-network rows are used
for the window-width comparison of the five random-network pairs in Section 5.5.2 (rand-01 to rand-05 with 10 min
windows, rand-06 to rand-10 with 20 min windows).

| Column | Meaning |
|---|---|
| `instance_id`, `instance`, `seed`, `group` | Instance |
| `setting` | Factor changed with respect to the Leuven base setting leuven-01 |
| `vehicles`, `ptw_width_min`, `pb_requests`, `rt_requests`, `service_hours` | Instance settings (Table 2) |
| `three_phase_accepted_pb`, `three_phase_accepted_rt`, `three_phase_accepted` | Requests accepted by the three-phase framework |
| `fixed_served_pb`, `fixed_served_rt`, `fixed_served` | Requests served by the fully fixed service on the same requests |

## From the CSV to Fig. 10

- Acceptance rate of an instance = sum over its three seeds of the accepted requests / sum of the requests (PB, RT, or all).
  Markers show this mean; bars show the range of the per-seed rates. The dashed line is the fully fixed service.
- Panels: (a) fleet size = leuven-05, leuven-01, leuven-02; (b) demand volume = leuven-01, leuven-08;
  (c) PTW width = leuven-04, leuven-01, leuven-03; (d) PB:RT share = leuven-06, leuven-01, leuven-07.
- leuven-09 and leuven-10 have the same settings as leuven-01; their nine seeds together give the range of the base
  setting (50 to 64 accepted requests, mean 55.4).
- DTD and IVT per accepted request (Section 5.5.2) are in `../table4_fixed_service/` (`three_phase_dtd`, `three_phase_ivt`).
