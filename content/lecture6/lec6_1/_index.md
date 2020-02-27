---
title: "Filters"
date: 2020-02-13T15:12:33-05:00
draft: false
weight: 1
---

When we add a layer to the map using the map.addLayer method, we have the ability to filter which parts of the spatial data are shown.

We'll be using older filter expressions: 
https://docs.mapbox.com/mapbox-gl-js/style-spec/other/#other-filter

But Mapbox has recently rolled out "new" expressions ... probably best to learn these - but I didn't have time before lecture!:
https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/

For vector tiles:
```js 
‘filter’: [<LOGIC>,<ATTRIBUTENAME>, <value>] 
```

 * Logic: ‘==’, ‘!=‘, ‘>’, ‘<’, ‘≥’, etc.
 * Attribute name: the name of an attribute your file has – check studio
 * Value: can be a string, numeric, boolean

For example:


``` 
‘filter’: [“>”, “income”, 100000] 
```

Translates to:

income > 100000

#### What if we want two conditions 
* spatial objects with a property > x but < y
* Use the combining filter method:

```javascript
[
  "all",
  [">", <ATTRIBUTE>, <LESSER_VALUE>],
  ["<=", <ATTRIBUTE>, <GREATER_VALUE>]
]

[
  "all",
  [">", ‘population’, 100000],
  ["<=", ‘population’, 2000000]
]
```

#### How do we combine different types of logic?

Combining Filters
```
["all", f0, ..., fn] logical AND: f0 ∧ ... ∧ fn
["any", f0, ..., fn] logical OR: f0 ∨ ... ∨ fn
["none", f0, ..., fn] logical NOR: ¬f0 ∧ ... ∧ ¬fn
```
Where f0 is a filter that looks like:
```
[logic, attribute, value]
```
