---
title: "Data/Styles in MapBox"
date: 2020-01-29T09:25:57-05:00
draft: false
weight: 2
---

#### Data in Mapbox
* When we go to Data we can [upload our own spatial files](https://docs.mapbox.com/help/troubleshooting/uploads/#accepted-file-types-and-transfer-limits)
  * MBTiles, KML, GPX, GeoJSON, Shapefile (zipped), CSV, GeoTIFF
* [If the file is vector data it will convert to a vector tile](https://docs.mapbox.com/vector-tiles/specification/)
  * PBF (mapbox vector tile format – “Protocolbuffer Binary Format”)
* If the file is raster data it will convert to a raster tile
  * PNGs

[EXAMPLE – Toronto Area Food Retailers (Points, geojson)](supermarkets.geojson)

[EXAMPLE – US States (Polygons, geojson)](TorontoDAs.geojson)


#### Styling the Data

* We can access the data we uploaded in the style section
  * Edit colors, other traits
* Limits to this method
  * Need javascript to do more complicated styling

* We can also download the whole thing as a json file
  * Mapbox GL style spec
  * https://www.mapbox.com/mapbox-gl-style-spec/
  * Open up example to see what else you can edit

## EXERCISE

* Add Toronto CMA, Toronto DAs, and Toronto Supermarkets as new tilesets
  * Create a new style
* Add the three data layers
  * Make CMA visible at low zoom levels (higher altitude)
  * Make DAs visible at medium zoom levels
  * Add supermarkets, and stylize
* Publish your map
