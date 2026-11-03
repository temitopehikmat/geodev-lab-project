## Data note

| Dataset | Source link | Geometry | Features | Key columns |Gaps noticed |
|---|---|---|---|---|---|
| Ward boundaries(clipped to Somolu) | https://data.grid3.org/datasets/GRID3::grid3-nga-operational-wards-v4-0/about  | Polygon | 9335 (national file); 16 after clipping to somolu | `state`, `statecode`, `lga`, `ward`, area_sqm (plus `source`, `date`, `editor`) |The key columns don't have nulls, but some other columns like lga_alt_na, ward_alt_na, ward_v1_gr are mostly nulls |

| LGA boundary (Somolu) | https://data.grid3.org/datasets/GRID3::grid3-nga-operational-lga-boundaries/about | Polygon | 774 (national file); 1 after clipping to Somolu | statename, statecode, lganame, lgacode (plus `source`, `timestamp`, `editor`, `uniq_id`)  | No null value in the key column but a column named amapcode has some missing values; Visible timestamps are from 2018 to 2019  |

| State boundary (Lagos) |  https://data.grid3.org/datasets/GRID3::grid3-nga-operational-state-boundaries-/about | Polygon |  37 (national file: 36 states plus FCT) | `statename`, `statecode`, `capcity`, `geozone` (plus `source`, `timestamp`, `editor`)  | Visible timestamps are from 2018 to 2019; `source` reads eHA_Polio; In statename, All 37 state names are unique |

| Settlement extents v4.1 | https://data.grid3.org/datasets/GRID3::grid3-nga-settlement-extents-v4-1/about  | Polygon | 7,387 downloaded; 803 after clipping to Somolu | `block_id`, `building_count`, `extent_type`, `mgrs_code`| No admin (state/LGA) fields; no population field |

| Settlement names | https://data.grid3.org/datasets/GRID3::grid3-nga-settlement-names/about  | Point | 292438 (national file); 24 after clipping | wardname, wardcode, lganame, lgacode, statename, statecode, set_id, set_name | 2020 data, older than the rest; timestamps are from 2016 to 2021; the key columns don't have no nulls, but some of the columns like is_primary, set_altname have nulls |

| Population v3.0 | https://data.grid3.org/maps/6966d625aea0488496d01debd3bb80f9/about | Raster, about 100 m cells (EPSG:4326) | Not applicable (grid) | Band `pop_updated`, values 0.67 to 1,204 per cell | Modelled estimates, not census counts. Clipped by rectangle, so it includes cells just outside Somolu |

| Rail stations (OSM) | https://www.openstreetmap.org (QuickOSM, `railway`=`station`, Lagos State extent, 2 Nov 2026) | Point, line, polygon | 14 point / 4 lines / 2 polygons| name, railway, public_transport, operator, network | operator and network mostly NULL; some stations mapped twice (point and outline) |

| Rail tracks (OSM) | https://www.openstreetmap.org (QuickOSM, `railway`=`rail`, Lagos State extent, 2 Nov 2026) | Line | 124 |  `railway`, `usage`, `gauge`, `electrified`, `surface`, `tunnel`, `passenger_lines`, `official_name` | Only `railway` and `gauge` are mostly filled. The rest have many NULLs |

### Notes
- **Clipping and file size.** The national wards file (157 MB) and the national population raster are not in this repository. Only the files clipped to Somolu are included, with links to the originals above.
- **Duplicate stations.** OSM maps some stations twice. The four station lines (Marina, Iganmu, Alaba, Mile 2) repeat points that already exist, and the Agege polygon repeats the Agege point. I will use the 14 points for distances, to avoid counting any station twice. [State what you decided about the Asiwaju Bola Tinubu polygon.]
- **Which stations count.** The `network` and `operator` fields are mostly empty, so I will identify Red Line stations by name: Agbado, Iju, Agege, Ikeja, Oshodi, Mushin, Yaba and Oyingbo. The points also include Blue Line stations and Mobolaji Johnson (Ebute Metta). I will test the question with Red Line stations only, then with all stations.
- **Population.** These are modelled estimates, not census counts. I will count residents per ward using zonal statistics, and the settlement extents will be used to see where people live, not for numbers of people.
- **Distance method.** All layers are in EPSG:4326, which measures in degrees. Before measuring, I will reproject to a metric CRS (UTM zone 31N, EPSG:32631), so the 2 km distances are correct. Distances are straight-line, not along roads.
- **OSM quality.** OpenStreetMap is volunteer-mapped, so station and track coverage may be uneven. Map data © OpenStreetMap contributors.
- **Settlement names.** This 2020 dataset is older than the others, so I use it only for labels.