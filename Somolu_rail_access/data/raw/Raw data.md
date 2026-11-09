# Raw data

Untouched downloads, as they came from the source. Every file derived from them is in `data/processed`. Three of the six files are too large for GitHub, so they are not in this repository. Download them again from the links below.

| File | What it is | Source | Size | In this repo? |
|---|---|---|---|---|
| GRID3_NGA_operational_wards_v4_0_618....zip | Ward boundaries for all of Nigeria (v4.0) | https://data.grid3.org/datasets/GRID3::grid3-nga-operational-wards-v4-0/about | 157 MB | No: over GitHub's 100 MB limit |
| GRID3_NGA_settlement_extents_v4_1_390....zip | Settlement extents v4.1, filtered on the GRID3 map to a view around Somolu (7,387 features) | https://data.grid3.org/datasets/GRID3::grid3-nga-settlement-extents-v4-1/about | 3.3 MB | Yes |
| NGA_LGA_Boundaries_2_2609687066015....zip | LGA boundaries for all of Nigeria | https://data.grid3.org/datasets/GRID3::grid3-nga-operational-lga-boundaries/about | 2.7 MB | Yes |
| NGA_population_v3_0_gridded.zip | Population v3.0, gridded estimates for all of Nigeria (about 100 m cells) | https://data.grid3.org/maps/6966d625aea0488496d01debd3bb80f9/about | 44.7 MB | No: too large for browser upload |
| NGA_State_Boundaries_V2_-1923488705....zip | State boundaries for all of Nigeria | https://data.grid3.org/datasets/GRID3::grid3-nga-operational-state-boundaries-/about | 0.65 MB | Yes |
| Settlements_in_Nigeria_53372966287655....zip | Settlement names (points) for all of Nigeria | https://data.grid3.org/datasets/GRID3::grid3-nga-settlement-names/about | 29.8 MB | No: too large for browser upload |

## OpenStreetMap data
The railway data was downloaded with the QuickOSM plugin in QGIS on 2 November 2026 (keys `railway`=`station` and `railway`=`rail`, Lagos State extent). Those files are small, so they are in `data/processed`, not here. See `data/processed/README.md`. Map data © OpenStreetMap contributors.

## Getting the missing files
Open the source link, then use the Download button on the dataset page. Unzip the file into this folder.