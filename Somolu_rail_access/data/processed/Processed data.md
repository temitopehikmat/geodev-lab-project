# Processed data

Only `Somolu_analysis.gpkg` and the masked population raster are analysis-ready. The other files are earlier steps, kept so the work can be traced. The checks and decisions are in `DATA_PREP_NOTE.md`.

| File | CRS | What it is |
|---|---|---|
| Somolu_analysis.gpkg | EPSG:32631 | Analysis-ready: the six vector layers listed in section 6 |
| Somolu_Population_utm31N_masked.tif | EPSG:32631 | Analysis-ready: population raster masked to the 16 wards |
| Somolu_wards_utm31n.gpkg | EPSG:32631 | Wards, reprojected (layer somolu_wards) |
| Somolu_LGA_Projected.gpkg | EPSG:32631 | LGA boundary, reprojected (layer somolu_lga) |
| somolu_settlement_extents.gpkg * | EPSG:32631 | Settlement extents after Fix geometries (layer somolu_settlement_extents) |
| Somolu_Settlement_Extent_utm31N.gpkg | EPSG:32631 | Settlement extents, reprojected, before repair |
| Somolu_Settlement_Projected.gpkg | EPSG:32631 | Settlement names, reprojected (layer somolu_settlement_names) |
| Lagos_railway_stations_points_projected.gpkg | EPSG:32631 | Station points, reprojected (layer lagos_railway_stations) |
| Lagos_railway_rail_projected.gpkg | EPSG:32631 | Rail tracks, reprojected (layer lagos_railway_tracks) |
| Lagos_railway_stations_lines_projected.gpkg, Lagos_railway_stations_polygons_projected.gpkg | EPSG:32631 | Station lines (4) and polygons (2), reprojected. Not in the GeoPackage, because they repeat the points |
| Somolu_Population.tif | EPSG:4326 | Population clipped by rectangle, before reprojection |
| Somolu_Population_utm31N.tif | EPSG:32631 | Rectangle, reprojected, before masking |
| Somolu_wards.gpkg, Somolu_LGA.gpkg, Somolu_settlementpt.gpkg | EPSG:4326 | Clipped before reprojection |
| Somolu_Settlement_Extent.gpkg | EPSG:3857 | Settlement extents clipped before reprojection |
| LagosState_.gpkg * | EPSG:4326 | OSM stations as downloaded (points, lines, polygons) |
| Lagos_tracks_.gpkg * | EPSG:4326 | OSM rail tracks as downloaded |
| Lagos_state.gpkg * | EPSG:4326 | Lagos State boundary used as the QuickOSM download extent |
| *.aux.xml | | GDAL statistics files that QGIS writes beside the rasters |

Layers in `Somolu_analysis.gpkg` (all EPSG:32631): somolu_wards, somolu_lga, somolu_settlement_extents, somolu_settlement_names, lagos_railway_stations, lagos_railway_tracks.