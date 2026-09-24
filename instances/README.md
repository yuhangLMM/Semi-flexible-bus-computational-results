# Instances

`leuven/` and `random/` contain one JSON file per instance and seed (`<instance>_s<seed>.json`, 30 files each).
The Leuven travel times and requests were generated with REQreate from the real stop coordinates; the random
networks were generated with the instance generator developed for this study (Section 5.1 of the paper).

## File format

| Key | Content |
|---|---|
| `config` | Service period (`window_start`, `window_end`, min after midnight), number of vehicles, vehicle capacity |
| `network.stops` | Stop indices along the corridor |
| `network.coordinates` | Stop coordinates (longitude, latitude) |
| `network.mandatory_stops`, `network.optional_stops` | Mandatory and optional stops |
| `network.terminals`, `network.city_center` | Terminal stops and city-center stops |
| `network.travel_times` | Travel time (min) between stops `"i,j"` |
| `network.dwell_times` | Dwell time (min) at each stop |
| `fleet` | Vehicles, trips per vehicle, capacity |
| `requests.prebooked`, `requests.dynamic` | PB and RT requests: `id`, `origin`, `destination`, `desired_time` (min after midnight), `time_window` (PTW, min), `request_time` (submission time, min after midnight of the service day; negative values are submissions on earlier days) |
| `parameters` | Operating hours and rejection penalty (1000); the Leuven files also give the PTW allowances (`promise_window`, ±5 min) and two plotting fields that are not used |

The random-network files also contain `generation` (generator settings) and a few generator fields in `config`.

## Mapping to the internal names

`instance_mapping.csv` has one row per instance file:

| Column | Meaning |
|---|---|
| `instance_id` | Public name, e.g. `leuven-01_s1` |
| `instance`, `seed` | Instance name (Table 2) and seed (1, 2 or 3) |
| `group` | `Leuven` or `random` |
| `internal_instance` | Internal instance folder (`final_update_instance_XX` for Leuven, `rand-XX__<name>` for the random networks) |
| `internal_seed_label` | Internal file label: `original` = seed 1, `seed_101` = seed 2, `seed_202` = seed 3 |
| `note` | For leuven-09 and leuven-10, seeds 2 and 3 use requests generated with request seeds 901/902 and 1001/1002 |
| `sha256` | SHA-256 hash of the instance file |
