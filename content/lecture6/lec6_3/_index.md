---
title: "Mouse Move Event Example"
date: 2020-02-13T15:12:58-05:00
draft: false
weight: 3
---

### Let's try this out with a mousemove event.

* We can use the mousemove  event to highlight a spatial object when our mouse is hovering over it.
* What we need:
  * Standard HTML file
  * Javascript file with
  * standard map object code
  * Standard add source code
  * Standard add layer code
* Things that are a bit different:
  * We need a second add layer code section
  * We will use the filter option to initially display NO spatial objects from the layer
  * As the mouse moves, we will change the filter so that it triggers the display of spatial objects over which the mouse hovers

```javascript

mapboxgl.accessToken = '<your access Token>';
var map = new mapboxgl.Map({
    container: 'map', //container id in HTML
    style: 'mapbox://styles/mwidener/cjcouhmq03m9t2rmvgnmmsr1l',  //stylesheet location
    center: [-102.542951,59.650162],  // starting point, longitude/latitude
    zoom: 2.5 // starting zoom level
});

//SIMPLY ADDING A POLYGON OF PROVINCES FROM MAPBOX VECTOR TILES
map.on('style.load', function(){

    map.addSource('provinces',{
        'type': 'vector',
        'url': 'mapbox://mwidener.6sokce8y'
    });

    map.addLayer({
        'id': 'provinces-fill',
        'type': 'fill',
        'source': 'provinces',
        'layout': {},
        'paint': {
            'fill-color': 'red',
            'fill-opacity': 1,
            'fill-outline-color': 'white'
        },
        'source-layer': "CanadianProvinces-5onu90"
    });

    //Add another visualization of the polygon of provinces. Note we do not add the source again!
    map.addLayer({
        'id': 'provinces-hl', //remember to change the name - this is our "highlight" layer (hence '-hl')
        'type': 'fill',
        'source': 'provinces',
        'layout': {},
        'paint': {
            'fill-color': 'grey',
            'fill-opacity': 1,
            'fill-outline-color': 'black'
        },
        'source-layer': "CanadianProvinces-5onu90",
        'filter': ["==","PRID",""] //Here is a filter that doesn't select anything
    });
    map.addLayer({
        'id': 'provinces-hl-lowpop', //remember to change the name - this is our "highlight" layer (hence '-hl')
        'type': 'fill',
        'source': 'provinces',
        'layout': {},
        'paint': {
            'fill-color': 'green',
            'fill-opacity': 1,
            'fill-outline-color': 'white'
        },
        'source-layer': "CanadianProvinces-5onu90",
        'filter': ["==","PRID",""] //Here is a filter that doesn't select anything
    });
    map.addLayer({
        'id': 'provinces-hl-highpop', //remember to change the name - this is our "highlight" layer (hence '-hl')
        'type': 'fill',
        'source': 'provinces',
        'layout': {},
        'paint': {
            'fill-color': 'blue',
            'fill-opacity': 1,
            'fill-outline-color': 'white'
        },
        'source-layer': "CanadianProvinces-5onu90",
        'filter': ["==","PRID",""] //Here is a filter that doesn't select anything
    });    
})

//*********************************
//HOVER EVENTS 1
//*********************************
map.on('mousemove', 'provinces-fill', function(e) {
    var features = e.features;  //e is passed to the function - 'e' is the event info triggered
    if(features.length > 0){ //if there are features in the e.features array then go into the conditional
        var feature = e.features[0];  //pull out the first feature element in the features array
        console.log(feature.properties)  //print out the feature properties in the browser console
        if(feature.properties.POP > 1000000){  //if the POP attribute of the features is > 1 mill, make it blue
            map.setPaintProperty("provinces-hl","fill-color","blue");
            console.log('pop is: ' + feature.properties.POP); //print pop value in console
        }
        else{
            map.setPaintProperty("provinces-hl","fill-color","green"); //if POP is less than 1 mill, make it green
            console.log('pop is: ' + feature.properties.POP); //print pop value in console
        }
        map.setFilter("provinces-hl",["==", "PRID", feature.properties.PRID]); //set the filter of the provinces-hl to display
                                                                               //the feature you're hovering over
    }
});


map.on('mouseenter','provinces-fill',function(e){   //when your mouse enters the provinces-fill layer
       map.getCanvas().style.cursor = 'pointer';    //change the mouse cursor to a pointer
       });
map.on('mouseleave','provinces-fill',function(e){
    map.getCanvas().style.cursor = '';                 // when the mouse leaves the provinces fill layer
    map.setFilter("provinces-hl",["==", "PRID",""]);   //change back to normal cursor, also remove filters to make
                                                       //provinces-hl layer invisible
});
//*********************************
//HOVER EVENTS 1
//*********************************




//*********************************
//HOVER EVENTS VERSION 2
//*********************************
/*map.on('mousemove', function(e){
    var features = map.queryRenderedFeatures(e.point, {
        "layers": ["provinces-fill"]}
    );
    if(features.length > 0){
        var feature = features[0];
        console.log(feature.properties)
        if(feature.properties.POP > 1000000){
            map.setPaintProperty("provinces-hl","fill-color","blue");
            console.log('pop is: ' + feature.properties.POP);
        }
        else{
            map.setPaintProperty("provinces-hl","fill-color","green");
            console.log('pop is: ' + feature.properties.POP);
        }
        map.setFilter("provinces-hl",["==", "PRID", feature.properties.PRID]);
    }
});
map.on('mouseenter','provinces-fill',function(e){
       map.getCanvas().style.cursor = 'pointer';
       });
map.on('mouseleave','provinces-fill',function(e){
    map.getCanvas().style.cursor = '';
}); */
//*********************************
//HOVER EVENTS VERSION 2
//*********************************


```
