---
title: "Introduction to TURF"
date: 2020-03-12T15:04:40-04:00
draft: false
weight: 10
chapter: true
pre: "<b>8. </b>"
---

#### Introduction

Mapbox GL JS is plenty powerful by itself. However, it doesn't have a lot of the classic spatial analysis tools that we've come to know and love (e.g. buffers).

[TURF](https://turfjs.org) is a library that works with geojson files. It allows you to conduct a number of spatial analysis operations in the web map environment.

Generally, TURF is lightweight and fast. It is composed of multiple modules that focus on specific types of operations. It also allows you to work locally with your geojson files for fast computation.

However, it's important to note:
#### TURF only works with geojson and NOT vector tiles.

#### Data for today's class:
* [Canadian Airports](canadianAirports.geojson)
* [Canadian Provinces](canadianProvinces.geojson)
* [UTM to UTSG Route](utmToUTSG.geojson)
