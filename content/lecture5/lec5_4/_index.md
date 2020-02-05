---
title: "Adding Layers"
date: 2020-02-05T09:53:30-05:00
draft: false
weight: 4
---

OK, so now we've added data, but the data are not yet displayed in the map. We have to tell mapbox how we want these data to be presented.

To do this we use the addLayer() method.

https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/

### For geojson:

```javascript
map.addLayer({
'id': 'a_layer_name_as_string',
'type': 'fill', //this can be fill for polygon, line for lines, or circle for points
'source': 'the_source_ID_from_addSource()',
'layout': {},
'paint': {    //a bunch of parameters that allow you to customize the display
  'fill-color': '#f08',
  'fill-opacity': 0.4
  }
});
```

### For vector:
```javascript
map.addLayer({
'id': 'a_layer_name_as_string',
'type': 'fill', //this can be fill for polygon, line for lines, or circle for points
'source': 'the_source_ID_from_addSource()',
'layout': {},
'paint': {    //a bunch of parameters that allow you to customize the display
  'fill-color': '#f08',
  'fill-opacity': 0.4
},
"source-layer": "some_layer_label_from_mapbox_data_page"
});
```

Refer to the above documentation link for which paint options you can use for different types of geometries.
