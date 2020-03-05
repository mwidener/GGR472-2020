---
title: "Adding a legend..."
date: 2020-02-27T11:13:02-05:00
draft: false
weight: 4
---

### Let's add a legend to our choropleth map!

To do this, we'll want to move to our HTML document. In mapbox gl js, our legend is going to be an HTML element layered on top of our map. To achieve this we need to use the <div> tag to define a division where the legend will go, and the <style> tag to define how the legend will look.

The <div> tag defines a division in the HTML document. Recall, we're already doing this with the following code to create a place for our webmap: ```<div id='map' class='map'> </div>```.

In this code we create a division element with an id we call 'map', and then assign it a class of 'map', which refers to the styling defined in within the <style> tag. We could modify the "#map" part of the style section in the HTML to mess with how the map is displayed in the window.

### How do we add a legend?

First we want to modify the style tags in our HTML code to add three new style guides:

* .legend
* .legend h4
* .legend div span

The first addition will dictate how the whole legend division is styled. The second will effect anything that used the <h4> tag. The third will effect anything in a <div> or <span> tag. More simply, .legend establishes the style norms for the legend object, .legend h4 establishes style norms for the legend title, and .legend div span will establish norms for the circle objects showing different colors in the legend.

```html
<style>
body { margin:0; padding:0; }

#map { position:absolute; top:0; bottom:0; width:100%; }

.legend {
  background-color: #fff;
  border-radius: 3px;
  bottom: 30px;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  font: 32px/32px 'Helvetica Neue', Arial, Helvetica, sans-serif;
  padding: 20px;
  position: absolute;
  right: 10px;
  z-index: 1;
}

.legend h4 {
  margin: 0 0 10px;
}

.legend div span {
  border-radius: 50%;
  display: inline-block;
  height: 20px;
  margin-right: 5px;
  width: 20px;
}
</style>
```

Next, we need to insert the actual <div> tags. Before we just had a <div> for the map and then the line pointing the html file to the .js code. Now we insert the following to make a legend:

```html
<body>
  <div id='map' class='map'> </div>
  <!-- Legend goes here! -->
  <div id='legend' class='legend'>
    <h4>Median Income</h4>  <!-- Legend title -->
    <div><span style="background-color: #edf8fb"></span>$0-$30,000/no data</div> <!-- a 'subdivision showing a colored circle and then text describing it' -->
    <div><span style="background-color: #b2e2e2"></span>$30,000-$50,000</div>
    <div><span style="background-color: #66c2a4"></span>$50,000-$70,000</div>
    <div><span style="background-color: #2ca25f"></span>$70,000-$90,000</div>
    <div><span style="background-color: #006d2c"></span>> $90,000</div>
  </div>
  <!-- Legend ends here -->
  <script src='./choropleth_legend-2020.js'></script>
</body>
```

Notice how the colors correspond exactly to the colors we selected when making our choropleth map.

All together it will look like the below code. Try adjusting the various properties to see how they affect the way the legend looks. Try making the spacing between elements bigger and reducing the size of the text.

```HTML
<!DOCTYPE html>
<html>
<head>
  <meta charset=utf-8 />
  <title>Median Income in Toronto</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <script src="https://api.mapbox.com/mapbox-gl-js/v1.7.0/mapbox-gl.js"></script>
  <link href="https://api.mapbox.com/mapbox-gl-js/v1.7.0/mapbox-gl.css" rel="stylesheet" />
  <style>
  body { margin:0; padding:0; }

  #map { position:absolute; top:0; bottom:0; width:100%; }

  .legend {
    background-color: #fff;
    border-radius: 3px;
    bottom: 30px;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
    font: 24px/20px 'Helvetica Neue', Arial, Helvetica, sans-serif;
    padding: 20px;
    position: absolute;
    right: 10px;
    z-index: 1;
  }

  .legend h4 {
    margin: 0 0 10px;
  }

  .legend div span {
    border-radius: 50%;
    display: inline-block;
    height: 20px;
    margin-right: 5px;
    width: 20px;
  }
  </style>

</head>
<body>
  <div id='map' class='map'> </div>
  <div id='legend' class='legend'>
    <h4>Median Income</h4>  <!-- Legend title -->
    <div><span style="background-color: #edf8fb"></span>$0/no data</div> <!-- a 'subdivision showing a colored circle and then text describing it' -->
    <div><span style="background-color: #b2e2e2"></span>$30,000</div>
    <div><span style="background-color: #66c2a4"></span>$50,000</div>
    <div><span style="background-color: #2ca25f"></span>$70,000</div>
    <div><span style="background-color: #006d2c"></span>$80,000</div>
  </div>
  <script src='./choropleth_legend-2020.js'></script>
</body>
</html>

```
