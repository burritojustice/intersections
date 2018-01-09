# intersections

SF and NYC intersections, via [TIGER/Line® Shapefiles: Roads](https://www.census.gov/cgi-bin/geo/shapefiles/index.php?year=2017&layergroup=Roads) 

- import county TIGER file https://www.census.gov/cgi-bin/geo/shapefiles/index.php?year=2017&layergroup=Roads
-`Dissolve` roads by `FULLNAME` (`Vector -> Geoprocessing`) [10 secs for SF]
- remove Interstates, `I-`, `State Hwy`, `US Hwy`, `Fwy`, (at least for urban areas?), `Brg`, `Tun`l, `NULL`
- run `Line Intersections` on `FULLNAME` [one minute for SF]
- look for long streets of interest without intersections, parallel to streets with lots of intersections -- consider adding midpoints on long streets so parallel intersections don't get greedy
- use field calculation to make intersection name (new field, name it `intersect`, length `100`, ` concat("FULLNAME_1", ' & ', "FULLNAME_2")`
- run `Mean coordinates` on `intersect` to handle intersections with dual carriageways (aka Dolores St) -- [15 minutes for SF]
- generate 'Voronoi polygons' (in `Geometry tools`)  [x min]
- in field calculator, use `replace' to generate a new text field for display, remove `St`, `Av`, etc
- run unique color tool to generate non-adjacent colorIDs

