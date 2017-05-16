---
title: "Geospatial data"
weight: 30
---

## What is GIS?

GIS stands for Geographic Information Systems (or Sciences), and refers to the software and techniques used to view, analyse, create, and modify geographic data. We’ll be borrowing some GIS terminology and techniques for this workshop. Traditional GIS software like [ArcGIS Desktop](https://esri.com) and [QGIS](http://www.qgis.org/en/site/) are desktop-based, but these exercises will focus on open source web-based tools.

## Common data types

GIS data comes in two major types: raster and vector.

Vector data consists of points, lines and polygons, and is most commonly used to represent discrete objects such as boundary lines, roads, building outlines, points of interest, etc. The file formats typically used for vector data are Esri shapefiles (.shp), Keyhole Markup Language files (.kmz or .kml, commonly found in Google Earth), GeoJSON, and even tabular data like Comma Separated Values (.csv).

![Points, lines and polygons on a web map](/images/vector.jpeg)

Raster data represents data as a grid of values, and is most commonly used to represent continuous data such as elevation, satellite imagery, watershed depths, precipitation, scanned analog maps, etc. The file formats are similar to those of images (GeoTIFF, JPEG, etc.). In web maps, raster data is sometimes split into smaller tiles, hosted on a server, and brought into the map as an overlay. 

![Raster image of a digitized map superimposed on a web map](/images/raster.jpeg)

In this workshop, we'll be creating point data (vector) of historical businesses and incorporating raster data of a scanned fire insurance plan. 