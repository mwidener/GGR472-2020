---
title: "Select with Buffer Example"
date: 2020-03-26T10:02:45-04:00
draft: false
weight: 2
---

### In this example:

We will use TURF to creat a circular buffer around wherever we click our mouse. This uses both mouse events and the TURF library. Once the TURF buffer is created, we can select points that fall within (a spatial join) the buffer and do something with this information (in our case, recolor the points and produce a pop up).

``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset=utf-8 />
  <title>Select Supermarkets with Buffer using TURF</title>
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
  <script src='./supermarkets.geojson'></script>
  <script src='./bufferSelect.js'></script>
</body>
</html>
```

``` javascript
//DON'T FORGET TO ADD YOUR ACCESS TOKEN!

//Standard set up
var map = new mapboxgl.Map({
  container: 'map',
  style: 'mapbox://styles/mapbox/streets-v8',
  center: [-79.385811,43.655298],
  zoom: 9
});

//because we can click the map, change the cursor to a 'pointer' style
map.getCanvas().style.cursor = 'pointer';

//add the supermarkets point layer from the geojson file
map.on('style.load', function(){
  map.addSource('supermarketSource',{
    'type': 'geojson',
    'data': sprmkt
  });
  map.addLayer({
    'id': 'supermarketLayer',
    'type': 'circle',
    'source': 'supermarketSource',
    'layout': {},
    'paint': {
      'circle-color': 'red', //make our base supermarket layer small red points
      'circle-radius': 3,
      'circle-opacity': 0.75
    }
  });
});


//*********************************************************
//Generate buffer, find points within buffer,
//highlight points, and create pop up with info about points
//*********************************************************

//set up variables before real work starts
var tempClickBuffer = null;
var tempSprmkts = null;
var popup = new mapboxgl.Popup({
  closeButton: true,
  closeOnClick: false
});

//when you click the map, do the following.
//recall 'e' is an event data object: https://www.mapbox.com/mapbox-gl-js/api/#EventData
map.on("click", function(e) {
    //clean up variables if we've already clicked somewhere else.
    //check by seeing if there's geojson text in the tempClickBuffer variable
    if (tempClickBuffer != null){
      tempClickBuffer = null;
      tempSprmkts = null;
      map.removeLayer('tempClickBufferLayer'); //get rid of the old buffer
      map.removeSource('tempClickBufferSource'); //get rid of the old selected supermarkets
      map.removeLayer('selectedSprmkts'); //reset source
      map.removeSource('tempSprmkts'); //reset source
    }

//create a point geojson object from the event data - this creates a point where you clicked
    tempLngLat = [e.lngLat.lng,e.lngLat.lat]; //create an array that looks like: [lng,lat]
    //make an object that is a 'geojson' object from the point data
    var tempPt = {
      "type": "Feature",
      "properties": {},
      "geometry": {
        "type": "Point",
        "coordinates": tempLngLat
      }
    };

//create a buffer using the point geojson you just created, 1 km circular buffer
    tempClickBuffer = (turf.buffer(tempPt, 1, {units: 'kilometers'}));
    tempClickBuffer = turf.featureCollection([tempClickBuffer]);
//see what supermarkets (from the sprmkt geojson variable) are within the 'tempClickBuffer' geojson object you just created.
//this function generates a new featureCollection called 'tempSprmkts', which we will display later

    tempSprmkts = turf.pointsWithinPolygon(sprmkt,tempClickBuffer);

//if the array is not null, add a pop up centered on your click location
//that states the number of supermarkets within the clickBuffer
    if (tempSprmkts.features.length != null){
      popup.remove()
           .setLngLat(e.lngLat)
           .setHTML('The number of supermarkets within 1 kilometer of'+
                    ' where you clicked is: ' + tempSprmkts.features.length)
           .addTo(map)
    };

//center the  map on the point you clicked and zoom in, using 'easeTo' so it is animated
    map.easeTo({
      center: e.lngLat, //center on the point you clicked
      zoom: 12, //zoom to zoom level 12
      duration: 1000 //take 1000 milliseconds to get there
    })

//add the source and layer information of the buffer geojson (tempClickBuffer) and
//subset of supermarkets geojson (tempSprmkts) objects you created
    map.addSource('tempSprmkts',{
      'type': 'geojson',
      'data': tempSprmkts
    });
    map.addLayer({
      'id': 'selectedSprmkts',
      'type': 'circle',
      'source': 'tempSprmkts',
      'layout': {},
      'paint': {
        'circle-color': 'blue', //make our selected supermarket layer BIGGER BLUE points
        'circle-radius': 6,
        'circle-opacity': 1
      }
    });
    map.addSource('tempClickBufferSource',{
      'type': 'geojson',
      'data': tempClickBuffer
    });
    map.addLayer({
      'id': 'tempClickBufferLayer',
      'type': 'fill',
      'source': 'tempClickBufferSource',
      'layout': {},
      'paint': {
        'fill-color': 'white',
        'fill-opacity': .4,
        'fill-outline-color': 'black'
      }
    }, 'selectedSprmkts'); // insert the buffer behind the selectedSupermarkets layer


  });
```
