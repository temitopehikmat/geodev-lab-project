# My Geodev-Lab Africa project
Which wards in Somolu LGA, Lagos are more than 2 km (straight-line distance) from the nearest Red Line station, and how many residents live in them? 
Built over twelve months with GeoDev lab Africa, Cohort One.
See project brief.md for the full brief
## Status
Month 1 complete (Weeks 1 to 4). Distance analysis for Somolu done with a 2 km buffer around the eight Red Line stations. Residents per ward are not yet calculated.

## What is in this repository
| Week | What | Where |
|---|---|---|
| 1 | Project brief with a source link for every dataset | [PROJECT_BRIEF.md](PROJECT_BRIEF.md) |
| 2 | Data note describing what I downloaded | [Data_Note.md](Data_Note.md) |
| 2 | Data as downloaded, clipped to Somolu | [data/](data/) |
| 3 | Data preparation and five quality checks | [DATA_PREP_NOTE.md](DATA_PREP_NOTE.md) |
| 3 | Analysis-ready GeoPackage | [Somolu_analysis.gpkg](Somolu_rail_access/data/processed/Somolu_analysis.gpkg) |
| 3 | Masked population raster | [Somolu_Population_utm31N_masked.tif](Somolu_rail_access/data/processed/Somolu_Population_utm31N_masked.tif) |
| 4 | Analysis results (buffer, ward classes) | [Somolu_week4_results.gpkg](Somolu_rail_access/data/processed/Somolu_week4_results.gpkg) |
| 4 | Map | [week4_wards_beyond_2km.png](screenshots/week4_wards_beyond_2km.png) |
| 4 | Month 1 summary | [month-1-summary.md](month-1-summary.md) |

Week 3 files are in `Somolu_rail_access/data/` (`raw` and `processed`). Week 2 files are in `data/`.

## Data sources
GRID3 Nigeria (ward, LGA, state boundaries, settlement extents and names, population), and OpenStreetMap via the QuickOSM plugin in QGIS (railway stations and tracks). Links and versions are in the brief.

## Tools
QGIS with the QuickOSM plugin.

## Credits
Map data © OpenStreetMap contributors. Population estimates: WorldPop / University of Southampton, distributed through GRID3.
