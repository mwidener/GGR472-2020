---
title: "Using TURF"
date: 2020-03-12T15:05:08-04:00
draft: false
weight: 2
---

It's important to look at all the tools in the library and develop a game plan.

Also, remember that because we’re in javascript, we can also program our own analysis tools ... and use the TURF library as your building blocks! Just add math!

### To start using TURF...

You must start by adding a line of code to your HTML file to say we’re adding the TURF library, and point to the codebase using a script tag. (If you ever want to add different javascript libraries you’d also do it this way).

Notice in the HTML below there is the standard reference to the mapbox gl js code, and then a new script tag for TURF.

``` html
<script src='https://api.mapbox.com/mapbox-gl-js/v1.8.1/mapbox-gl.js'></script>
<link href='https://api.mapbox.com/mapbox-gl-js/v1.8.1/mapbox-gl.css' rel='stylesheet' />
<script src='https://npmcdn.com/@turf/turf/turf.min.js'></script>
```

Now in our javascript we can use TURF to analyze our geojson feature. Remember we need to access our geojson file on a server, but since we're working from home, you can use the following code to add the geojson files you'll need:

With the geojson file we can pick out individual features within the geosjon file to do things like calculate:
* Distance
* Area
* Bounding box

We can also use TURF to relate geojson features to one another
* Count of points in polygon
* Distance between regions
* Intersections
