## The question
Which wards in Somolu LGA, Lagos are more than 2 km (straight-line distance) from the nearest Red Line station, and how many residents live in them? 
## Study area 
Somolu Local Government Area, Lagos State, Nigeria. Stations outside the LGA boundary are included, because a ward's nearest station may lie across the border.
## Why it matters 
Wards far from a station have less access to rail commuting. Transport planners in Lagos could use the results to decide where feeder bus routes or shuttles would serve the most people.
## The data
| Dataset | Source and version | Link |
|---|---|---|
| Ward boundaries | GRID3 NGA Operational Wards v4.0 (Oct 2026), 157 MB national file | https://data.grid3.org/datasets/GRID3::grid3-nga-operational-wards-v4-0/about |
| LGA boundaries | GRID3 NGA Operational LGA Boundaries (Dec 2020), 2.6 MB | https://data.grid3.org/datasets/GRID3::grid3-nga-operational-lga-boundaries/about |
| State boundaries | GRID3 NGA Operational State Boundaries (Dec 2020), 646 KB. Used to set the Lagos State download extent | https://data.grid3.org/datasets/GRID3::grid3-nga-operational-state-boundaries-/about |
| Settlement extents | GRID3 NGA Settlement Extents v4.1 (Aug 2026), 3.3mb. Clipped to Somolu| https://data.grid3.org/datasets/GRID3::grid3-nga-settlement-extents-v4-1/about |
| Settlement names | GRID3 NGA Settlement Names (Sept 2020), 29.8mb | https://data.grid3.org/datasets/GRID3::grid3-nga-settlement-names/about |
| Population | GRID3 NGA Population v3.0, about 100 m grid (WorldPop / University of Southampton, 2025), 44.66mb | Clipped to Somolu | https://data.grid3.org/maps/6966d625aea0488496d01debd3bb80f9/about |
| Railway stations | OpenStreetMap via QuickOSM, key `railway`=`station`, Lagos State extent, downloaded 2 Nov 2026 | https://www.openstreetmap.org |
| Railway tracks | OpenStreetMap via QuickOSM, key `railway`=`rail`, Lagos State extent, downloaded 2 Nov 2026 | https://www.openstreetmap.org |
Map data © OpenStreetMap contributors.
## What I would build
A map of Somolu's wards coloured by distance to the nearest Red Line station, with wards beyond 2 km flagged and their resident counts shown. It could be updated whenever new stations open.
