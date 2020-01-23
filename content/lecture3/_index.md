+++
title = "Lecture 3: Data, cont."
date = 2020-01-22
weight = 5
chapter = true
pre = "<b>2. </b>"
+++

# Recall js objects?

```js
var mycar = "subaru";

// name: value pairs (name/value separated by colon)
var mycar = {
	make: "Subaru",
	model: "Impreza",
	year: 2005,
	states_provinces_driven_through: ["ontario", "new york", "michigan"];
};
```

#### What would this return?

```js
mycar.make
```

#### This leads us to geoJSON: Geographic Java Script Object Notation

##### GeoJSON is a simple open standard used to store spatial features, alongside non-spatial features.


```javascript
{ "type": "FeatureCollection",
    "features": [
      { "type": "Feature",
        "geometry": {"type": "Point", "coordinates": [102.0, 0.5]},
        "properties": {"prop0": "value0"}
        },
      { "type": "Feature",
        "geometry": {
          "type": "LineString",
          "coordinates": [
            [102.0, 0.0], [103.0, 1.0], [104.0, 0.0], [105.0, 1.0]
            ]
          },
        "properties": {
          "prop0": "value0",
          "prop1": 0.0
          }
        },
      { "type": "Feature",
         "geometry": {
           "type": "Polygon",
           "coordinates": [
             [ [100.0, 0.0], [101.0, 0.0], [101.0, 1.0],
               [100.0, 1.0], [100.0, 0.0] ]
             ]
         },
         "properties": {
           "prop0": "value0",
           "prop1": {"this": "that"}
           }
         }
       ]
     }
```



