---
title: "GeoJSON polygons"
date: 2020-01-22
chapter: true
weight: 3
---

#### Polygons can be quite complicated.

#### GeoJSON allows for an easy way to describe polygons with (multiple) interior gaps.

* Polgyon
	* LinearRing (exterior)
		* Positions
	* LinearRing (interior)
		* Positions
	* LinearRing (interior)
		* Positions

#### Only 1 exterior ring and then as many interior rings as needed

```javascript
{ "type": "Polygon",
	"coordinates": [
			[[35,10], [45,45], [15,40], [10,20],[35,10]],
			[[20,30], [35,35], [30,20], [20,30]]
		]
}
```
#### Care also should be taken with coordinate ordering in GeoJSON Polygons

##### The exterior ring should be counterclockwise
##### Interior rings should be clockwise

#### Why does this matter?

##### The classic Chamberlain & Duquette algorithm for calculating the area of a polygon on a sphere has the nice property that *counterclockwise-wound polygons have positive area and clockwise yield negative.* If you ensure winding order, calculating the area of a polygon with holes is as simple as adding the areas of all rings.
##### Winding order also has a default meaning in Canvas and other drawing APIs: *drawing a path with counterclockwise order within one with clockwise order will cut it out of the filled image.*

[source: More than you ever wanted to know about geojson](http://www.macwright.org/2015/03/23/geojson-second-bite.html)
