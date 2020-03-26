---
title: "Choropleth Grid and Clustered Points"
date: 2020-03-26T10:02:50-04:00
draft: false
weight: 1
---

### In this example:

We will use TURF to count the number of airport points that exist within each grid cell.

Then we'll use the code we learned about previously to color the grid cells based on the number of airports inside.

Finally, we will use the mapbox feature that allows points to cluster at various zoom levels. This is useful if you have lots of points scattered all over the place. At low resolutions nearby points will group together. At higher resolutions they will separate.

``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset=utf-8 />
  <title>Airport Hex Bins</title>
    <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
    <script src="https://api.mapbox.com/mapbox-gl-js/v1.9.0/mapbox-gl.js"></script>
    <link href="https://api.mapbox.com/mapbox-gl-js/v1.9.0/mapbox-gl.css" rel="stylesheet" />
    <script src='https://npmcdn.com/@turf/turf/turf.min.js'></script>

  <style>
    body { margin:0; padding:0; }
    #map { position:absolute; top:0; bottom:0; width:100%; }
  </style>
</head>
<body>

<div id='map' class='map'> </div>


<script src='canadianAirports.geojson'></script>
<script src='./turfExample2.js'></script>
</body>
</html>
```

## Remember to use your own access token and mapbox style
``` javascript
//ADD YOUR ACCESS TOKEN!!!!!!!!

var map = new mapboxgl.Map({
    container: 'map',
    style: 'mapbox://styles/mwidener/cjcotwplq3loj2ss0pjqmmigh',
    center: [-90, 52],
    zoom: 3
});

//CREATE A SQUARE GRID
var bbox = turf.bbox(canadianAirports);//extent method returns bounding box in order:
//minX (West), minY(South), maxX (East), maxY (North)
var cellSide = 50; //in the units you defined above
var options = {units: 'kilometers'}; //units that will determine the width of the square grid
var airport_squaregrid = turf.squareGrid(bbox, cellSide, options); //makes the new geojson squaregrid features

//COUNT THE NUMBER OF AIRPORTS IN EACH SQUARE BIN
//This function collects the properties from the point layer and 'collects' them into the polygon layer
//In this case, we are collecting all of the FEATUREID properties from the canadianAirports. For
//each square, there will be a collection of FEATUREIDs from the airports that are within them
//HINT: look at the squareAirports geojson featurecollection you've created in the javascript console
var squareAirports = turf.collect(airport_squaregrid,canadianAirports, "FEATUREID","AIRPORTNAMES");



//Now we need to count the number of features inside of each square, and also figure out the largest
//number of airports in any one of our squares
var max_airports_in_square = 0;
squareAirports.features.forEach(function(square){
    square.properties.AIRPORTCOUNT = square.properties.AIRPORTNAMES.length; //calculate the length of the collected FEATUREIDs - this gives us the number of points in each square
    if (square.properties.AIRPORTCOUNT > max_airports_in_square){
        max_airports_in_square = square.properties.AIRPORTCOUNT; //update the max number of airports in a square
    }
});


//Standard map.on section, where we load the airport point file
map.on('style.load', function(){
    map.addSource('airports',{
        "type": "geojson",
        "data": canadianAirports,
        "cluster": true,            //use the cluster function available for geojson points
        "clusterMaxZoom": 10,
        "clusterRadius": 30
    })
    map.addLayer({
        "id": "airportsLayer",
        "type": "circle",
        "source": "airports",
        "layout": {},
        "paint":{
            'circle-color': "black",
            'circle-radius': {
                base: 10,
                stops: [[5, 10], [22, 180]]}, //adjust size of point at diff zoom levels
            'circle-opacity': 1
        }
    });

    // Now we can add our square grid ... it was generated before the map was displayed
    map.addSource('airportGrid',{
        "type": "geojson",
        "data": squareAirports  //this is the square grid WITH the collect attribute
    });
    map.addLayer({
        "id": "airportSquareGrid-layer",
        "type": "fill",
        "source": "airportGrid",
        "layout": {},
        "paint":{
          "fill-color": [
            'interpolate',
            ['linear'],
            ['to-number',['get', 'AIRPORTCOUNT'],0], // get a number, but if provided with a non-number default to 0
            0, '#ffffcc',
            1, '#c7e9b4',
            2, '#7fcdbb',
            4, '#41b6c4',
            8, '#2c7fb8',
            max_airports_in_square, '#253494'
          ],  
            'fill-opacity': .5
        }
    },"airportsLayer"); //insert these layers BEFORE the point file so that the airport point file is on top
});
```
