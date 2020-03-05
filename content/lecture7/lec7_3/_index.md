---
title: "Choropleth Maps"
date: 2020-02-27T11:12:58-05:00
draft: false
weight: 3
---

### What if we want to visualize the spatial information embedded in our spatial layers?

* Thankfully, building choropleth maps has become relatively easy in Mapbox.
* Before, it was necessary to either add multiple layers with filters either manually or programmatically.
  * For example:
    * layer 1 all provinces with population less than 300,000 are light red
    * layer 2 all provinces with population more than 300,000 and less than 1,000,000 are red
    * layer 3 all provinces with population more than 1,000,000 are dark red

Now it's much easier thanks to the interpolate tool:
https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate

* We can integrate some code about interpolating between colors given some data input into the fill-color property of a fill layer.

### [Relevant example from mapbox](https://docs.mapbox.com/mapbox-gl-js/example/updating-choropleth/)

* Helpful hint: to find the color scheme for your map, use [colorbrewer](http://colorbrewer2.org)
* Let's try the following using the following [example data: median income DAs](toronto_censusDA_income.geojson).

#### [Example](http://ggr472.geog.utoronto.ca/~widenerm/week_7/choropleth_no_legend-2020.html)

```javascript
var map = new mapboxgl.Map({
  container: 'map',
  style: 'mapbox://styles/mapbox/streets-v8',
  center: [-79.45312, 43.7],
  zoom: 10
});


map.on('style.load', function(){
  //Normal add source code
  map.addSource('toronto_DAs', {
    'type': 'vector',
    'url': 'mapbox://mwidener.aipfqxb4'
  });
  map.addLayer({
      "id": "DA-layer",
      "type": "fill",
      "source": "toronto_DAs",
      "source-layer": "toronto_censusDA_income-3p3din",
      "paint": {
          "fill-color": [
            'interpolate',
            ['linear'],
            ['to-number',['get', 'medIncome'],0], // get a number, but if provided with a non-number default to 0
            0, '#edf8fb',
            30000, '#b2e2e2',
            50000, '#66c2a4',
            70000, '#2ca25f',
            80000, '#006d2c'
          ],
          "fill-opacity": 0.8,
          "fill-outline-color": 'black'
      }
    });
});

// FIRST ADD A POPUP OBJECT
var popup = new mapboxgl.Popup({
        closeButton: false,
        closeOnClick: false
});

// NEXT DEFINE WHEN YOU WANT THE POPUP TO HAPPEN
map.on('mousemove','DA-layer', function(e){
    popup.remove(); //If a popup already exists, get rid of it!

    //get the rendered features that belong to the provinces-fill layer
    var features = map.queryRenderedFeatures(e.point, {
        "layers": ["DA-layer"]}
    );
    //if there is a feature there, do the following
    if (features.length > 0){
        console.log(features[0]); //print out the first element of the features array that was selected
        var feature = features[0]; //store the first element as 'feature'
        popup.setLngLat(e.lngLat); //place the popup window at the lng and lat where your click event happened
        //add stuff to the pop up:
        popup.setHTML("<b>The median income here is: $</b>" + feature.properties.medIncome + "<br>");
        popup.addTo(map); //finally add the pop up to the map

    }
    //if there are no features under the click, then print this in the web browser console
    else{
        console.log("no features from layer here...")
    }
});

```
