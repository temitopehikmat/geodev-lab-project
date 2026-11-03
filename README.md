# My Geodev-Lab Africa project
Which wards in Somolu LGA, Lagos are more than 2 km (straight-line distance) from the nearest Red Line station, and how many residents live in them? 
Built over twelve months with GeoDev lab Africa, Cohort One.
See project brief.md for the full brief
## Status
Week 2: data downloaded, opened in QGIS, clipped to the study area and described. The distance and population analysis comes next.

## What is in this repository
- [PROJECT_BRIEF.md](PROJECT_BRIEF.md): the question, study area, why it matters, and every dataset with its source link
- [Data_Note.md](Data_Note.md): for each dataset, the source, geometry type, feature count, key columns and gaps
- `data/`: the datasets, clipped to Somolu (the national files are too large for GitHub, so see the links in the brief)
- `screenshots/`: the project open in QGIS

## Data sources
GRID3 Nigeria (ward, LGA, state boundaries, settlement extents and names, population), and OpenStreetMap via the QuickOSM plugin in QGIS (railway stations and tracks). Links and versions are in the brief.

## Tools
QGIS with the QuickOSM plugin.

## Credits
Map data © OpenStreetMap contributors. Population estimates: WorldPop / University of Southampton, distributed through GRID3.
