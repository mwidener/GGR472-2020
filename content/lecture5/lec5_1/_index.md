---
title: "Adding Data"
date: 2020-02-05T09:53:38-05:00
draft: false
weight: 1
---

### It's easy to add data from a range of sources to your mapbox map.
* Vector (from your data page on mapbox)
* Raster (from your data page on mapbox)
* GeoJSON from your server/another website
* Images/Videos

### Must use asynchronous call.
#### This is a way to keep code from running until some event occurs.

```javascript
map.on('load', function(){
  // DO STUFF HERE
});
```

In the 'DO STUFF HERE' area we want to do two things.

1) Add the data source - where are we pulling data from to put in our site?
2) Draw the data.

How do we do this? Let's look at the API to see what the addSource() and addLayer() methods do!

https://www.mapbox.com/mapbox-gl-js/api/
