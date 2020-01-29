---
title: "My 1st MapBox Map"
date: 2020-01-29T12:59:38-05:00
draft: False
weight: 5
---

To make our map we'll need at least some HTML code and JavaScript code. We could do it all in one file, but for organizational reasons, we'll create an HTML file and another file for our JavaScript.

### Setting up your html file.

The below code has the basics that we'll need to set up our map.

``` HTML
<!DOCTYPE html>
<html>
<head>  
   <meta charset=utf-8 />  
   <title>TITLE HERE – shows up in browser tab</title>  
   <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />  <!-- Adjusts the screen width to the device accessing the web map -->
   <script src="https://api.mapbox.com/mapbox-gl-js/v1.7.0/mapbox-gl.js"></script> <!-- Sets up Mapbox GL JS -->
   <link href="https://api.mapbox.com/mapbox-gl-js/v1.7.0/mapbox-gl.css" rel="stylesheet" /> <!-- Sets up Mapbox GL JS -->
   <!-- below - in file CSS browser set up -->
   <style>
      body { margin:0; padding:0; }   
      .map { position:absolute; top:0; bottom:0; width:100%; }  
   </style>
</head>
<body>  <!-- where we put our javascript code -->
   <div id='map' class='map'> </div>  <!-- browser set up -->
   <script src='./MYJAVASCRIPTCODE.js'></script> <!-- "./" means current directory, so if you put your code elsewhere use that path -->
</body>
</html>

```

### Setting up your JavaScript file.

``` JavaScript
mapboxgl.accessToken = '<YOUR ACCESS TOKEN HERE>';
var map = new mapboxgl.Map({  
   container: 'map',  //container id in HTML
   style: 'mapbox://styles/mapbox/streets-v8',  //stylesheet location
   center: [-96.7, 60.00],  // starting point, longitude/latitude
   zoom: 3 // starting zoom level
});
```
### Let's try this for real...
* Create HTML/JS code to create a map and then post it on your website.
  * Create a new style and use that path for your new map.
