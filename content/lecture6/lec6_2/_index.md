---
title: "Events"
date: 2020-02-13T15:12:54-05:00
draft: false
weight: 2
---

### Let's start with mouse events

* The mouse is the primary mode of interaction with the computer
 * Essential for navigating webpages, web maps, web apps, etc.
* Modern browsers pay close attention to what the mouse is doing
 * Hover, clicks
* Take advantage of this to add interface

![old computer mouse](https://www.computinghistory.org.uk/userdata/images/large/86/66/product-78666.jpg)

* Events are things that happen to elements in the webpage
 * Can be something done by the browser or user
 * JS can react to events and implement code

* We’ve been doing this already with:

```javascript

map.on('load', function(){
	stuff;
});

```

* Essentially the code is listening for events to happen
	* knows what to implement when that event happens

We can look at all of the event types here: 
https://docs.mapbox.com/mapbox-gl-js/api/#events

And the specific events under map in the API here:
https://docs.mapbox.com/mapbox-gl-js/api/#map
