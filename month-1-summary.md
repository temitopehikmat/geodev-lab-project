# Month 1 summary

## Question
Which wards in Somolu LGA, Lagos are more than 2 km (straight-line) from the nearest Red Line station, and how many residents live in them?

## Operation and why
I buffered the eight Red Line stations (Oyingbo, Yaba, Mushin, Oshodi, Ikeja, Agege, Iju, Agbado) by 2,000 m in EPSG:32631, with 32 segments per quarter circle, and dissolved the result into one polygon of 92.17 km². I then ran Extract by location on the 16 wards. "Beyond 2 km" is my strict definition: no part of the ward touches the buffer (disjoint). The other wards intersect it.

I chose a buffer because it tests the 2 km rule directly, and one merged polygon covers "nearest of any station" without comparing every ward with every station. I selected the stations by name, because the operator and network fields are mostly empty, and I did not clip them to Somolu, because the nearest stations (Mushin and Yaba) lie outside the LGA. The distance is straight-line, so it ignores roads, canals and the lagoon.

## What I expected and what I got
**Expected:** I wrote this after I had drawn the buffer over the wards, not before. I expected about 9 wards to touch the buffer and about 7 to lie fully outside it.

**Got:** 5 wards beyond 2 km and 11 touching the buffer (5 + 11 = 16). The five beyond wards are Apelehin, Aiyetoro/Mafowoku, Seriki-Okuta, Ilaje and Akoka/Anu-Oluwapo.

After seeing the result I added a share-of-area measure (`pct_in_buffer`) and four classes. The 10% and 90% cut-offs are my judgement, set after I saw the values. Ibuowo/Owotutu (11.5%) is close to the 10% line.

| Class | Wards | Count |
|---|---|---|
| Beyond 2 km | Apelehin, Aiyetoro/Mafowoku, Seriki-Okuta, Ilaje, Akoka/Anu-Oluwapo | 5 |
| Marginal (under 10% inside) | Owode/Orile Bariga (0.09%), Igbari (1.88%) | 2 |
| Partly served (10 to 90%) | Ibuowo/Owotutu (11.5%), Bajulaiye (35.3%), Pedro/Gbagada (45.3%), Okesuna/Alase (47.6%) | 4 |
| Mostly served (90% or more) | Bashua East & West, Igbobi/Fadeyi, Ijebu Tedo, Onipanu, Orile Somolu/Alade | 5 |

Map: `screenshots/week4_wards_beyond_2km.png`

## Four checks
1. **Look at the map.** The five beyond wards lie fully outside the buffer circles. The wards in the other classes touch or sit inside them. The two marginal wards (Owode/Orile Bariga and Igbari) show only a sliver inside the circle edge.
2. **Row count against expectation.** 5 beyond + 11 within = 16. I expected about 7 beyond and got 5. I had counted Owode/Orile Bariga and Igbari as outside by eye, but the tool found that they touch the buffer.
3. **One feature checked by hand** (Measure Line, Cartesian, meters, snapped to vertices):
   - **Owode/Orile Bariga to Mushin:** 1,995.98 m by hand. The distance field gives 1,975.64 m. Both are under 2,000 m, so the ward is within 2 km. The hand reading is longer because I clicked a vertex, while the closest point may lie along an edge.
   - **Akoka/Anu-Oluwapo to Yaba:** 2,205.61 m by hand. The distance field gives 2,205.60 m. Both are over 2,000 m, so the ward is beyond 2 km.
   - My first Akoka measurement started from the wrong station (Mushin) and a far corner, and read 2,894 m. My second try read 2,203.71 m, which is shorter than the true shortest distance and so cannot be right. I think that click snapped to a vertex of a different layer. My third measurement agrees with the distance field.
4. **Empty geometry.** I ran `is_empty_or_null($geometry)` on the buffer and on the three ward layers (`wards_beyond_2km`, `wards_within_2km`, `wards_access_class`). Every feature returned false. I also confirmed that `redline_stations` has 8 features.

**Distance cross-check.** I calculated the straight-line distance from every ward to its nearest Red Line station. All 5 beyond wards are above 2,000 m, from 2,205.6 m (Akoka/Anu-Oluwapo) to 3,439.8 m (Ilaje). All 11 others are below 2,000 m. The buffer and the distance method agree on all 16 wards.

## What surprised me
- Only 5 of 16 wards are beyond 2 km, fewer than I expected when I first looked at the map.
- Owode/Orile Bariga (0.09% inside) and Igbari (1.88% inside) touch the buffer only by a sliver. Under my strict rule they count as within 2 km, even though the buffer barely covers them. Owode/Orile Bariga is 1,975.6 m from Mushin, so about 24 m separates it from "beyond", which is the same order as the error in an OSM station point.
- Most wards are nearest to Mushin, but Igbari and Akoka/Anu-Oluwapo are nearest to Yaba. Every nearest station is outside Somolu.
- Akoka/Anu-Oluwapo is only about 206 m beyond the threshold, so its class also depends on where the Yaba point sits.

## What data I still need
- **Residents per ward.** I have not calculated residents, so the second half of my question is still open. The next step is zonal statistics (sum) on the masked population raster for the 5 beyond wards. The 16 ward sums should add up to 211,849.65. The population is a modelled estimate, well below the 2006 census figure of 403,569, so any count will be reported as an estimate.
- **Road network distance**, because straight-line distance ignores roads, canals and the lagoon.
- **A check of the 16-ward list** against an official ward list.
- **A review for new Red Line stations** opened since the OSM download on 2 Nov 2026.
- **A repeat with all stations** (Blue Line and NRC) to compare with the Red Line result.