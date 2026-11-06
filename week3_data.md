
# Week 3: data preparation note

Project: rail access in Somolu LGA, Lagos. Question: which wards are more than 2 km (straight-line) from the nearest Red Line station, and how many residents live in them? Prepared 5 November 2026.

## 1. Working CRS

**EPSG:32631 (WGS 84 / UTM zone 31N)**

- **Metres.** The 2 km threshold needs distances in metres. EPSG:4326 uses degrees.
- **Fits the area.** Somolu is at about 3.4 degrees east, close to the centre of UTM zone 31N (0 to 6 degrees east), so distortion is very small.
- **Same datum.** EPSG:32631 and the source data (EPSG:4326) both use WGS 84, so no datum shift was involved.
- **Why not EPSG:3857.** The settlement extents arrived in Web Mercator (EPSG:3857), which stretches distances away from the equator. The same Somolu layer measured about 0.6% wider and 1.4% taller in EPSG:3857 than in EPSG:32631.

## 2. What I reprojected and clipped

| Layer | Source CRS | Clipped to | Before clipping | After clipping | After reprojection |
|---|---|---|---|---|---|
| Ward boundaries (GRID3 v4.0) | EPSG:4326 | Somolu LGA | 9,335 | 16 | 16 |
| LGA boundary (GRID3) | EPSG:4326 | Somolu LGA | 774 | 1 | 1 |
| Settlement extents (GRID3 v4.1) | EPSG:3857 | Somolu wards | 7,387 | 803 | 803 |
| Settlement names (GRID3) | EPSG:4326 | Somolu LGA | 292,438 | 24 | 24 |
| Rail stations, points (OSM) | EPSG:4326 | Not clipped | 14 | 14 | 14 |
| Rail tracks (OSM) | EPSG:4326 | Not clipped | 124 | 124 | 124 |
| Population raster (GRID3 v3.0) | EPSG:4326 | Rectangle around the wards, then masked with the ward polygons after reprojection | National raster | 47 x 48 cells (rectangle) | 1,186 valid cells (masked) |

- **Stations and tracks were not clipped.** The nearest station to a Somolu ward can lie outside the LGA, so Lagos-wide data was kept.
- **Station lines (4) and polygons (2) were also reprojected** to EPSG:32631, but they are not in the analysis GeoPackage. They repeat stations that are already mapped as points.
- **Population raster method.** The rectangle clip was reprojected with Nearest neighbour resampling, which keeps the original cell values. Then Clip Raster by Mask Layer cut it to the exact shape of the 16 wards.

**Population raster at each step**

| | Rectangle (EPSG:4326) | Reprojected (EPSG:32631) | Masked to wards (EPSG:32631) |
|---|---|---|---|
| Cell size | 0.000833 degrees (about 92 m) | 92.13 m | 92.13 m |
| Cells with data | 2,126 (94.24% of 47 x 48) | 2,126 | 1,186 |
| Minimum / maximum per cell | 5.08 / 1,118.68 | 5.08 / 1,118.68 | 5.72 / 1,118.68 |
| Mean per cell | 160.02 | 160.02 | 178.63 |
| Sum | 340,194.82 | 340,194.82 | 211,849.65 |

- **Reprojection did not change the total** (difference 0.00%), because each old cell maps to one new cell.
- **The rectangle's total is not Somolu's population.** It includes cells outside the wards. After masking, the sum of 211,849.65 is the modelled population of the area covered by the 16 wards, about 10.07 km² (1,186 cells x 92.13 m x 92.13 m). Resident counts per ward will come from zonal statistics.

## 3. The five quality checks

Run on the downloaded data, before reprojecting and clipping.

| Check | What I looked at | What I found | Fixed or flagged, and why |
|---|---|---|---|
| Completeness | Whether each dataset covers Somolu and the stations that could serve it. Compared the OSM stations with the LAMATA Red Line map and fact sheet. | 16 wards for Somolu; 803 settlement-extent features after clipping; the population raster covers the study area. The OSM points include all eight Red Line stations: Oyingbo, Yaba, Mushin, Oshodi, Ikeja, Agege, Iju and Agbado. The track layer has 124 segments, and few carry a name. | Accepted: station coverage is enough for the question. Flagged: the 16 wards are GRID3 operational wards and were not compared with an official ward list. |

| Currency | The release date of each dataset and the OSM download date. | Wards v4.0: October 2026. Settlement extents v4.1: August 2026. Population v3.0: 2025 modelled estimates. LGA and state boundaries: December 2020 (record timestamps 2018 to 2019). Settlement names: 2020. OSM rail data: downloaded 2 November 2026. | Flagged the 2020 boundary and settlement-name files, and the modelled population. The Red Line has been in commercial service since October 2024. The result describes the stations in service at the 2 November 2026 download. OSM edit dates for individual features are unknown. |

| Positional accuracy | The CRS and extent of every layer; how the stations line up with the LAMATA map and satellite imagery; whether the LGA and ward boundaries match. | Settlement extents arrived in EPSG:3857, the others in EPSG:4326. The LGA (2020) and ward (2026) extents agree within about 1.5 m on the west, north and south edges, but the LGA outline reaches about 32 m further east. OSM maps some stations more than once (as a point, a line and a polygon). | Fixed: all analysis layers were reprojected to EPSG:32631. Flagged: the east-edge difference. The ward layer defines the analysis units, and 32 m does not matter for a 2 km threshold. Flagged: duplicate station shapes, so the 14 point features are used. |

| Attribute accuracy | The attribute tables of the stations, tracks, settlement extents and boundaries. | `network` and `operator` are mostly empty in the station layer. Some stations belong to the Nigerian Railway Corporation (NRC) and not the Red Line, for example Mobolaji Johnson (Ebute Metta, in the points) and Asiwaju Bola Tinubu (Apapa, in the polygons). The points also include Blue Line stations (Marina, Iganmu, Mile 2, Alaba, National Theatre). Settlement extents hold block-level fields such as `block_id`, building counts and `extent_typ`; some blocks have zero buildings. | Fixed: Red Line stations are selected by name from the LAMATA list of eight, and Blue Line and NRC stations are excluded from the main test. Flagged: settlement extents describe settlement blocks, not buildings or population. |

| Fitness for purpose | Whether each dataset can answer the question, including whether the population total is plausible. | Ward polygons suit ward-level results. Station points suit straight-line distance. The population raster (cells of about 92 m) suits a 2 km threshold, but its values are modelled. Its total over the wards (211,849.65, about 21,000 people per km²) is below published figures: 403,569 in the 2006 census and a 2022 projection of 597,400 (citypopulation.de), over a published LGA area of 14.6 km². Settlement extents show where built-up areas are but hold no population. Tracks are display data. | Kept the wards, Red Line station points and population raster for the main analysis. Flagged the population gap: resident counts will be reported as modelled estimates, with this comparison stated. Settlement extents and tracks are context only. Straight-line distance ignores roads, canals and the lagoon, and the question is limited to the Red Line. |

## 4. Technical checks

| Check | Method | Result |
|---|---|---|
| CRS | Layer Properties, Information tab | Wards, LGA, settlement extents, settlement names, stations (points, lines, polygons), tracks and the population raster all report EPSG:32631 with units in metres. |
| Feature counts | Compared before and after reprojection | Unchanged for every layer (section 2). |
| Geometry validity | Processing Toolbox, Check validity (GEOS), on the six GeoPackage layers | See the table below. |
| Duplicate geometries | Processing Toolbox, Delete duplicate geometries, on the six GeoPackage layers | See the table below. |

| Layer | Valid | Invalid | Duplicates removed |
|---|---|---|---|
| somolu_wards | 16 | 0 | 0 |
| somolu_lga | 1 | 0 | 0 |
| somolu_settlement_extents | 801 (803 after repair) | 2 (0 after repair) | 0 |
| somolu_settlement_names | 24 | 0 | 0 |
| lagos_railway_stations | 14 | 0 | 0 |
| lagos_railway_tracks | 124 | 0 | 0 |

Two settlement-extent polygons were invalid. I repaired them with Fix geometries, and a re-check found 0 invalid, with the count unchanged at 803. All other layers were valid. The station lines (4) and polygons (2), which stay outside the GeoPackage, were also valid. Station shapes that repeat across the point, line and polygon layers are different representations of the same station. They were handled by using the points, not by deleting them

## 5. Problems found and decisions

| # | Problem | Fixed or flagged | What I did and why |
|---|---|---|---|
| 1 | The first ward reprojection still reported EPSG:4326 | Fixed | The Target CRS had defaulted to the project CRS. I re-ran the tool with EPSG:32631 chosen explicitly and checked the result: 16 features, EPSG:32631, units in metres. |
| 2 | Settlement extents were downloaded in EPSG:3857 | Fixed | Reprojected to EPSG:32631, because Web Mercator overstates distances and areas. |
| 3 | OSM maps some stations more than once | Flagged | The 14 point features are used for distances, so no station is counted twice. |
| 4 | `network` and `operator` are mostly empty, and NRC stations have names similar to Red Line stations | Fixed | Red Line stations are selected by name from the LAMATA list. Blue Line and NRC stations are excluded from the main test. |
| 5 | The LGA outline reaches about 32 m further east than the ward layer | Flagged | The wards define the units of analysis, and the gap is negligible for a 2 km threshold. |
| 6 | The first population clip was a rectangle, so its total included cells outside Somolu | Fixed | After reprojection I masked the raster with the ward polygons. The masked sum (211,849.65) covers only the area of the 16 wards. |
| 7 | The modelled population is well below published figures | Flagged | The raster covers about 10.07 km² against a published 14.6 km² for the LGA, and its density is lower than census-based figures. I kept it, and will compare ward totals from zonal statistics with this sum. Results will be reported as modelled estimates with this gap stated. |
| 8 | Several datasets are old or modelled | Flagged | The 2020 boundaries, the 2020 settlement names and the 2025 modelled population were accepted for a 2 km access question. |
| 9 | The count of 16 wards was not checked against an official list | Flagged | GRID3 operational wards may differ from electoral wards. This will be checked when results are reported. |

| 10 | Two settlement-extent polygons had invalid geometry | Fixed | Repaired with Fix geometries. The re-check found 0 invalid features and the count stayed at 803. Invalid polygons can give wrong results in clipping and area calculations, so I fixed them before packaging. |

## 6. Analysis-ready files

`data/processed/Somolu_analysis.gpkg`

| Layer | Geometry | Features | CRS | Role |
|---|---|---|---|---|
| somolu_wards | Polygon | 16 | EPSG:32631 | Units of analysis |
| somolu_lga | Polygon | 1 | EPSG:32631 | Study area outline |
| somolu_settlement_extents | Polygon | 803 | EPSG:32631 | Context |
| somolu_settlement_names | Point | 24 | EPSG:32631 | Labels |
| lagos_railway_stations | Point | 14 | EPSG:32631 | Distance targets |
| lagos_railway_tracks | Line | 124 | EPSG:32631 | Map display |

`data/processed/Somolu_Population_utm31N_masked.tif`: the population raster, EPSG:32631, cells of 92.13 m, masked to the 16 wards (1,186 valid cells). It stays a GeoTIFF because zonal statistics reads raster cell values.


