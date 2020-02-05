---
title: "Bringing it all together"
date: 2020-02-05T09:53:25-05:00
draft: false
weight: 5
---

Using the [supermarket geojson data](supermarket.geojson) from last week...

### geojson example:

```javascript
mapboxgl.accessToken = 'pk.eyJ1IjoibXdpZGVuZXIiLCJhIjoibXBKQU85dyJ9.Q6yf1zk7wpnYqpsQfRwVmw';
var map = new mapboxgl.Map({
   container: 'map', //container id in HTML
   style: 'mapbox://styles/mwidener/cikgx8tbm003tapm5o1zquc9m',  //stylesheet location
   center: [-79.39, 43.72],  // starting point, longitude/latitude
   zoom: 10 // starting zoom level
});

map.on('style.load', function(){
/*ADDING A SOURCE FROM A GEOJSON FILE*/
  map.addSource('supermarket_data',{
    'type': 'geojson',
    'data': './supermarket.geojson'
  });

  map.addLayer({
    'id': 'supermarket_points',
    'type': 'circle',
    'source': 'supermarket_data',
    'layout': {},
    'paint': {
      'circle-color': 'yellow',
      'circle-radius': 2,
    }
  });

  /*ADDING A SOURCE FROM A MAPBOX TILESET - DATA YOU UPLOADED TO MAPBOX STUDIO*/
  map.addSource('supermarket_data_vector',{
    'type': 'vector',
    'url': 'mapbox://mwidener.ck629gt2v0bkm2jmqhtcc41uw-0zmtf'
  });
  map.addLayer({
    'id':'supermarket_points_vector',
    'type': 'circle',
    'source': 'supermarket_data_vector',
    'layout': {},
    'paint': {
        'circle-color': 'red',
        'circle-radius': 4
    },
    'source-layer': 'supermarkets' //get this from mapbox tileset page
  }, 'supermarket_points');

});
```

### vector data example:
