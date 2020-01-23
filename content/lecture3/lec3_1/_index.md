---
title: "GeoJSON components"
date: 2020-01-22
chapter: true
weight: 1
---

* A Feature type is a spatial object
	* Has geometry and properties
	* It is possible to have multiple geometries, but this is very rare
* A FeatureCollection type
	* Object that has feature objects


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
#### From [geojson.org](http://geojson.org):
* 2.2. Feature Objects
	* A GeoJSON object with the type "Feature" is a feature object.
	* A feature object must have a member with the name "geometry". The value of the geometry member is a geometry object as defined above or a JSON null value.
	* A feature object must have a member with the name "properties". The value of the properties member is an object (any JSON object or a JSON null value).
	* If a feature has a commonly used identifier, that identifier should be included as a member of the feature object with the name "id".
* 2.3. Feature Collection Objects
	* A GeoJSON object with the type "FeatureCollection" is a feature collection object.
	* An object of type "FeatureCollection" must have a member with the name "features". The value corresponding to "features" is an array. Each element in the array is a feature object as defined above.
