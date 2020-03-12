---
title: "Setting up geojson"
date: 2020-03-12T15:05:13-04:00
draft: false
weight: 3
---

### We need our geojson files to act like javascript variables.

How do we do this? All it takes is a simple tweak to the geojson file.

Simply add ```var mygeojsonfilename = ``` before the first curly bracket.

So for example:

``` javascript
var utmToUTSG = {
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {},
      "geometry": {
        "type": "LineString",
        "coordinates": [
          [
            -79.66263771057129,
            43.54487765059555
          ],
          [
            -79.65937614440918,
            43.54276236856476
          ],
          [
            -79.65568542480469,
            43.54126918362085
          ],
          [
            -79.65293884277344,
            43.53884267921116
          ],
          [
            -79.65105056762695,
            43.53598052284858
          ],
          [
            -79.64890480041502,
            43.53486051163794
          ],
          [
            -79.62607383728027,
            43.54773938461675
          ],
          [
            -79.62109565734863,
            43.54873473851718
          ],
          [
            -79.61766242980956,
            43.55215614218778
          ],
          [
            -79.6168041229248,
            43.55259157963129
          ],
          [
            -79.61302757263184,
            43.552218347729465
          ],
          [
            -79.61139678955078,
            43.552218347729465
          ],
          [
            -79.61088180541992,
            43.55582615929037
          ],
          [
            -79.60521697998047,
            43.56310332874207
          ],
          [
            -79.60375785827637,
            43.56478255071955
          ],
          [
            -79.59302902221678,
            43.574732535219056
          ],
          [
            -79.5736312866211,
            43.592203217066874
          ],
          [
            -79.5615291595459,
            43.60326743161359
          ],
          [
            -79.55225944519043,
            43.611471040985265
          ],
          [
            -79.54848289489746,
            43.61395676232749
          ],
          [
            -79.53972816467284,
            43.615386005576845
          ],
          [
            -79.51981544494629,
            43.61930071530575
          ],
          [
            -79.48419570922852,
            43.62675660019726
          ],
          [
            -79.47999000549316,
            43.62837192004496
          ],
          [
            -79.47535514831543,
            43.63185092304897
          ],
          [
            -79.47097778320312,
            43.63427368118269
          ],
          [
            -79.46591377258301,
            43.63688269609634
          ],
          [
            -79.46205139160156,
            43.63831139435743
          ],
          [
            -79.45638656616211,
            43.63911890443505
          ],
          [
            -79.4502067565918,
            43.638559860152576
          ],
          [
            -79.44419860839844,
            43.63700693207628
          ],
          [
            -79.43449974060057,
            43.63290700911552
          ],
          [
            -79.43098068237305,
            43.632472152394485
          ],
          [
            -79.4245433807373,
            43.633776713117946
          ],
          [
            -79.41329956054688,
            43.63706904996992
          ],
          [
            -79.41003799438477,
            43.63744175598323
          ],
          [
            -79.40291404724121,
            43.63775234256172
          ],
          [
            -79.3927001953125,
            43.63831139435743
          ],
          [
            -79.39209938049315,
            43.638559860152576
          ],
          [
            -79.39987778663635,
            43.657925383503695
          ],
          [
            -79.39809143543243,
            43.65827855515278
          ],
          [
            -79.39885318279266,
            43.660036620475
          ],
          [
            -79.39863324165344,
            43.6601103571893
          ],
          [
            -79.3995988368988,
            43.66243107697202
          ]
        ]
      }
    }
  ]
}
```

#### Next you need to reference this file in your HTML file.

Add the following to your HTML, inside the body tags. You can likely reference these files locally on your own hard drive, but if that doesn't work, you can use the links I have provided below:

``` HTML
<body>

<div id='map' class='map'> </div>

<!--Insert your geojson files here-->
<script src='https://mwidener.github.io/lecture8/utmToUTSG.geojson'></script>
<script src='https://mwidener.github.io/lecture8/canadianAirports.geojson'></script>
<script src='https://mwidener.github.io/lecture8/canadianProvinces.geojson'></script>

<script src='./turfExamples1.js'></script>
</body>
```

Now we can access these geojson files as variables (whatever you named them...in the above example I have three variables canadianAirports, canadianProvinces, and utmToUTSG).