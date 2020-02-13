---
title: "Mouse click event example"
date: 2020-02-13T15:13:02-05:00
draft: false
weight: 4
---

### Let's also try this with a mouse click event ... but try to figure this out on your own...

```javascript

mapboxgl.accessToken = '<your access token>';
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
//CLICK EVENTS VERSION 1
//*********************************
map.on('click','provinces-fill',function(e){
    var features = e.features;
    console.log('print: ' + features)
    if(features.length > 0){
        var feature = features[0];
        //console.log(feature)
        var current_filter = map.getFilter("provinces-hl");
        if(current_filter[2] == feature.properties.PRID){
            map.setFilter("provinces-hl",["==", "PRID", ""])
        }
        else{
            map.setFilter("provinces-hl",["==", "PRID", feature.properties.PRID]);
        }
    }
}); 
map.on('mouseenter','provinces-fill',function(e){
       map.getCanvas().style.cursor = 'pointer';
       });
map.on('mouseleave','provinces-fill',function(e){
    map.getCanvas().style.cursor = '';
});
//*********************************
//CLICK EVENTS VERSION 1
//*********************************



//*********************************
//CLICK EVENTS VERSION 2
//*********************************
/*map.on('click', function(e){
    //var point_test = e.point
    //console.log('blah: ' +point_test);
    var features = map.queryRenderedFeatures(e.point, {  //grab features from the point on which the event 'e' occurred
        "layers": ["provinces-fill"]}                    //we're only interested in features on provinces-fill layer
    );
    if (features.length > 0){            // if there are features to be clicked on (i.e. 1 or more)
        console.log(features[0]);       // print out the feature in the console
        var feature = features[0];      //move the feature into a variable
        var current_filter = map.getFilter("provinces-hl");  //get the current status of the provinces-hl filter
        if(current_filter[2] == feature.properties.PRID){    //if the filter is currently set to where we clicked
            map.setFilter("provinces-hl",["==", "PRID", ""]) //then we want to remove the filter (i.e. turn off a previous click)
        }
        else{
            map.setFilter("provinces-hl",["==", "PRID", feature.properties.PRID]); //otherwise, we want to set the filter to the                                                                        //feature we clicked on
        }
    }
    else{
        map.setFilter("provinces-hl",["==", "PRID", ""]);   //if features.length == that means we clicked off our feature layer
                                                            //so make hl layer invisible
    }
}); 
map.on('mouseenter','provinces-fill',function(e){
       map.getCanvas().style.cursor = 'pointer';
       });
map.on('mouseleave','provinces-fill',function(e){
    map.getCanvas().style.cursor = '';
}); */
//********************************* 
//CLICK EVENTS VERSION 2
//*********************************




```

