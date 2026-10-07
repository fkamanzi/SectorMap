# SectorMap

Turn a cell list into sector wedges on a map, check PCIs and neighbours, and export the sectors to QGIS, MapInfo or Google Earth. It runs in your browser.

**Use it here: https://fkamanzi.github.io/SectorMap/**

Open the link in Chrome or Edge on a laptop and drop your cell list in. There is nothing to install. The page opens with a made-up demo network so you can try it straight away.

If the link doesn't load on your network, download the ZIP from https://github.com/fkamanzi/SectorMap/archive/refs/heads/main.zip, unzip it, and open `index.html` in Chrome or Edge. It works the same way.

## Input

- One row per cell, from a CSV or text file, an Excel `.xlsx`, or rows pasted from Excel.
- Only latitude and longitude are required. Azimuth, beamwidth, band or layer, frequency (EARFCN or ARFCN), PCI, site and cell name are picked up when present.
- Columns are found automatically, including English, Portuguese, Spanish, French and Russian headers. You can change any of them under Columns.
- Coordinates can be decimal degrees, with a decimal point or a comma, or degrees, minutes and seconds with N, S, E or W. Cells without an azimuth are drawn as circles.

## On the map

- Sector wedges with the bands nested by length. The default length follows the spacing between your sites.
- Colour by any column, or by PCI mod 3, mod 6 or mod 30.
- Click a legend entry to hide it.
- Site, cell, PCI or band labels.
- Search by site or cell. Click a sector to see every column for that cell.
- Neighbour lines once you add a neighbour list with a source and a target cell column.
- A ruler for distance and bearing.

## Checks

| Check | What it lists |
|---|---|
| Rows not placed | Every row that could not go on the map, with the reason |
| Same PCI on the same frequency | Pairs closer than the distance you set |
| Same site, frequency and PCI mod 3 | Co-site pairs that share mod 3 |
| Cell names used more than once | Duplicate cells, with their rows |
| Sites whose rows disagree on location | Rows of the same site more than 100 m apart |
| Neighbour names not in the cell list | Relations that point to unknown cells |
| One-way neighbour relations | Relations defined in one direction only |

## Export

| Button | File | Opens in |
|---|---|---|
| Google Earth | `.kml`, one folder per legend entry | Google Earth, QGIS |
| QGIS | `.geojson` | QGIS, most GIS tools |
| Shapefile | `.zip` with `.shp`, `.shx`, `.dbf`, `.prj` and `.cpg` | QGIS, ArcGIS, MapInfo |
| MapInfo | `.zip` with `.mif` and `.mid` | MapInfo, QGIS |
| CSV with WKT | `.csv` | Excel, or QGIS as delimited text |

Every export carries all your columns plus the azimuth, beamwidth, sector length, colour and legend entry used for each sector. Coordinates are WGS84.

## Privacy

The page reads your list in the browser, and the list is never uploaded. The page downloads only the background map, from OpenFreeMap, and its content security policy blocks every other connection. Without a connection it shows a plain background, and the sectors, checks and exports work the same.

## Testing

- The calculations were checked against an independent reading of test lists in CSV, semicolon-separated text with decimal commas and degrees-minutes-seconds, Excel, UTF-16 text and pasted rows.
- Sector shapes were checked against WGS84 geodesics.
- Every export format was read back with GDAL, the library QGIS uses to open files.
- End-to-end runs in Chromium from a local file covered loading, checks, exports and the phone layout. A 100,000-cell list loads and is checked in seconds.
- Firefox and Safari have not been tested yet.

If your list doesn't load as expected, open an issue with the header row and one sample row, with anything sensitive masked.

## Credits

- [MapLibre GL JS](https://maplibre.org) 5.24.0, BSD 3-Clause licence.
- The Barlow Semi Condensed font, SIL Open Font License 1.1.
- Background maps from [OpenFreeMap](https://openfreemap.org), © [OpenMapTiles](https://www.openmaptiles.org/), data from [OpenStreetMap](https://www.openstreetmap.org/copyright).

The full licence texts are inside `index.html`.

This is an independent tool, not affiliated with or endorsed by any vendor or operator.

Version 1.0, 7 Oct 2026. Prepared by Frutos
