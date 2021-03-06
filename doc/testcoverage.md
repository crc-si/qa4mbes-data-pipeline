## Running coverage tests

`testcoverage` checks whether the bounding polygon of a survey swath intersects a planned survey region. If so, it returns:

- test start time
- test stop time
- planning polygon file name
- test swath file name
- percentage of planning area covered by swath
- area of the intersection of the planned and surveyed region in square metres
- distance between centroids of the planned and surveyedareas in metres
- minimum distance between polygons in metres
- the intersection boundary as GeoJSON in lat/lon (`EPSG:4326`); the percentage of planning

If the regions don't intersect at all, the `percentage`, `area` and `geometry` values are set to `None`.

If input polygon as shapefiles, or swath data as `.las`/`.laz` do not contain CRS information, a `QA failed` message is given, with the file name missing CRS information.

`testcoverage.py` currently works for `.xyz` and `las/laz` ungridded swath files; `tif/tiff` and `bag` gridded formats, using `.shp` or `.geoJSON` reference polygons:

`python qa4mbes/testcoverage.py -i "tests/xyzdata/4819-100000lines.xyz" -r "tests/gridcoverages/testcoverage.shp"`

### Caveats

- XYZ files *must* have 5 tab separated columns; with the first three columns being X, Y and Z respectively (lon, lat, depth).
- output geometries are always expressed in `EPSG:4326` (latitude, longitude)
- input `geoJSON` and `.xyz` files are **always** assumed to contain coordinates expressed in `EPSG:4326` (lat/lon).

### Examples:

See notebook examples for [point clouds](../notebooks/pointcloudcoveragetesting.ipynb) and [grids](../notebooks/gridcoveragetesting.ipynb)
