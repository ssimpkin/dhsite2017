---
title: "Adding data to Leaflet"
weight: 60
---

## Overview

[Leaflet](http://leafletjs.com/) is an open-source web mapping library that can display vector data (points, lines, and polygons) as well as raster overlays like our georectified maps. This intermediate-level exercise is designed to show how our different types of data can be integrated into a single interactive webmap.

### Data files
* [GeoJSON file with Rideau Street businesses](/files/leaflet-demo/businesses.geojson)
* [Leaflet example folder](/files/leaflet-demo.zip)

### Recommended software
* [Sublime Text](https://www.sublimetext.com)
* [SimpleHTTPServer](http://www.pythonforbeginners.com/modules-in-python/how-to-use-simplehttpserver/) (Mac), [MAMP](http://www.mamp.info/en/) (Mac) or [WampServer](http://www.wampserver.com/en/) (Windows)

{{< warning title="Watch out" >}}
We'll be creating offline Leaflet maps in this exercise, but it will be necessary to set up a local web server to load the data files (if your points don't appear after the test in step one, this is probably why). Options include running [SimpleHTTPServer](http://www.pythonforbeginners.com/modules-in-python/how-to-use-simplehttpserver/) in your Leaflet example folder, or installing [MAMP](http://www.mamp.info/en/) (Mac) or [WampServer](http://www.wampserver.com/en/) (Windows).
{{< /warning >}}

## Starting a web server (Mac)

First, download the leaflet-demo folder. Save it to your computer in an easily accessible location. I recommend adding the folder to your home directory, which you can open with the shortcut ```Shift - Command - H```. 

A local web server is necessary to run Leaflet offline in your browser. There's a Python-based one that is built into Mac computers called SimpleHTTPServer. It is a command line tool (but don't be afraid!).

Open a Terminal window by searching for "Terminal" in the Spotlight Search. You'll see a prompt where commands can be entered.

For this exercise, we need to navigate to the leaflet-demo folder to launch SimpleHTTPServer. If the leaflet-demo folder is in your home directory, it should be visible when we list the files.

Type ```cd``` in the prompt and press enter. This will make sure you start in the home directory.

Type ```ls``` in the prompt and press enter. This will list the contents of the directory.

If you see leaflet-demo in the list, navigate to it by typing ```cd leaflet-demo``` and pressing enter. 

Next, type ```python -m SimpleHTTPServer 8000``` and press enter to launch the web server. We'll keep the terminal window open in the background while we work on our Leaflet map.

To make sure everything is configured correctly, navigate to ```localhost:8000/leaflet-test.html``` in your web browser. You should see a map of Ottawa with points showing the Rideau Street businesses. Clicking on the points will open a pop-up window showing more details about the businesses. We'll be recreating this map today.

## Starting a web server (Windows)

Download and install [WampServer](http://www.wampserver.com/en/). You may be prompted to select your preferred web browser and text editor.

Launch WampServer from the Start menu. A green "W" icon should appear in your taskbar. Click on it and navigate to the ```www``` directory. 

Next, download the leaflet-demo folder, unzip it and move it to the ```www``` directory.

Click on the green "W" icon again and click on ```localhost```. This will launch your web browser. Navigate to ```localhost/leaflet-demo/leaflet-test.html```. You should see a map of Ottawa with points showing the Rideau Street businesses. Clicking on the points will open a pop-up window showing more details about the businesses. We'll be recreating this map today.

![Web map of Ottawa showing 1890-era businesses](/images/windows-map.jpg)

## Setting up your map

We'll be looking at a series of steps that build on each other to create a simple webmap.

Navigate to the ```leaflet-demo``` folder, then right click on the ```01.html``` file. Open it with a text editor, such as Sublime Text, Notepad (Windows), or TextEdit (Mac).

There are a few things happening in this code block.

```html```
<!-- 
  ****************************************************************************
  Leaflet demo map by Sarah Simpkin / sarahsimpkin@gmail.com
  Based on a tutorial by Andy Woodruff and Ryan Mullins: http://maptimeboston.github.io/leaflet-intro/
  STEP 1: Setting up the map
  ****************************************************************************
-->

<!-- ~ HTML code to set up the page where the map will go ~ -->
```

First, we use HTML code to provide some comments about the code we're using. Anything appearing between ```<!--``` and ```-->``` is considered a comment and will be invisible on the final webmap. 

```html
<html>
<head>
  <title>Ottawa web map</title>
```

Next, HTML code is used to give the page a title between the ```<title>``` and ```</title>``` tags. 

```html
<link rel="stylesheet" href="http://cdn.leafletjs.com/leaflet-0.7.3/leaflet.css"/>
  <script src="http://cdn.leafletjs.com/leaflet-0.7.3/leaflet.js"></script>
  <script src="jquery-2.1.1.min.js"></script>
```

Our webmap relies on some external styles and scripts. These are linked on the first few lines.

```css
      body { margin:0; padding:0; }
      #map { position:absolute; top:0; bottom:0; left:0; right:0; width:100%; }
```

Next, our webmap is given some dimensions on the page. Ours will take up the full browser window, so the margins have been set to 0 and the width has been set to 100%.

```html
<div id="map"></div>
```

A ```<div>``` element is created to hold our map.

```
  var map = L.map('map').setView([45.42621, -75.69243], 19);
```

Then the map is added and customized using Javascript. The view is set to focus on our desired coordinates (in this case, the corner of Rideau Street and Sussex Drive). The zoom level (set to 19) will zoom in the map to show the buildings up close. You can zoom out the default view by reducing this number.

```
  L.tileLayer('http://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png',
    {
      attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a> &copy; <a href="http://cartodb.com/attributions">CartoDB</a>',
      maxZoom: 20,
      minZoom: 1
    }).addTo(map);
```

To give the map a basemap layer showing streets, a tilelayer is loaded from the web. I've chosen a light grey basemap from CartoDB, but other basemaps are available for free online. A useful site for previewing these options is the [Leaflet-providers preview](https://leaflet-extras.github.io/leaflet-providers/preview/). It's important to acknowledge where the basemap layer came from, so Leaflet provides a space to include attribution information. You can also specify which levels of zoom should be available.


**Example 1 shows a light grey basemap from CartoDB**
<iframe src="/files/leaflet-demo/01.html" width="100%" height="540"> </iframe>


## Adding a GeoJSON file

Next, examine ```02.html``` in your text editor.

```
  // ~ Loads a GeoJSON file with our points ~
  $.getJSON("businesses.geojson",function(data){
    L.geoJson(data, {
      pointToLayer: function(feature,latlng){
        var marker = L.marker(latlng);
        return marker;
      }
    }).addTo(map);
```

This new section of code is responsible for bringing in the ```businesses.geojson``` file that is located in the same directory as the leaflet map. It reads the information in the file and adds markers on each point.


**Example 2 showing point data from businesses.geojson**
<iframe src="/files/leaflet-demo/02.html" width="100%" height="540"> </iframe>


## Adding pop-ups

To make the map more dynamic, we can add pop-ups to each marker that reveal more information about each business.

Open ```03.html``` in your text editor.

```
// ~ Make a pop-up, configure which attributes to display
        marker.bindPopup('<strong>' + feature.properties.business_name + '</strong></br>' + feature.properties.description); 
```

Only one line of code is required to bind the pop-ups to the markers. This section of code creates the pop-ups and specifies their content: two fields from ```businesses.geojson``` called ```business_name``` and ```description```. I've wrapped the business name in ```<strong>``` tags to make them appear in bold on the final map. 


**Example 3 with pop-ups**
<iframe src="/files/leaflet-demo/03.html" width="100%" height="540"> </iframe>


## Adding an overlay map

We can also include raster imagery from sources such as Map Warper.

![Export screen from Map Warper showing links](/images/mapwarper-export.jpeg)

Open a georectified map in [Map Warper](http://mapwarper.net).

Click on the ```Export``` tab, then copy the address in the ```Tiles (Google/OSM scheme)``` field.

The URL should look something like ```http://mapwarper.net/maps/tile/20531/{z}/{x}/{y}.png```.

This address can be pasted in the following code snippet to bring the image tiles into our Leaflet map. Just like the basemap layer, we can add attribution information and specify which zoom levels the imagery should appear in. 

```
  // ~ Loads a tile layer from Map Warper ~
  L.tileLayer('http://mapwarper.net/maps/tile/20531/{z}/{x}/{y}.png',
    {
      attribution: 'Tiles by <a href="http://mapwarper.net/maps/20531">Map Warper user sarahsimpkin</a>',
      maxZoom: 20,
      minZoom: 1
    }).addTo(map);
```

**Example 4 showing the raster overlay**
<iframe src="/files/leaflet-demo/04.html" width="100%" height="540"> </iframe>


