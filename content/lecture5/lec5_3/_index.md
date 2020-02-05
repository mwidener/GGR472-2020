---
title: "Adding Vector Data"
date: 2020-02-05T09:53:32-05:00
draft: false
weight: 3
---

If we want to add data from the Dataset section of our mapbox portal, we can make a direct reference to those data using the addSource() method.

```javascript
map.addSource('my_data',{
  "type": "vector",
  "url": "mapbox://mwidener.3259jdk2" //link to data from mapbox site
})
```

![add vector data](add_vector_data.png)
