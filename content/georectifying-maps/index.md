---
title: "Georectifying maps"
weight: 50
---

## Overview

Existing maps, floorplans and imagery are a useful source of data. They can provide information about changes over time, landcover, settlement patterns, and more. In this exercise, we'll use the web-based tool [Map Warper](https://mapwarper.net/) to add geographic coordinates to existing maps in order to view them alongside contemporary data.


### Data files
* [1901 Fire Insurance Plan of Ottawa](/files/georectify/FireInsurancePlan_1901.zip)
* [1842 Map of Bytown](/files/georectify/1842.jpg)
* [1856 Map of Ottawa](/files/georectify/1856.JPG)
* [1911 Map of Ottawa](/files/georectify/1911.JPG)
* [1933 Airphoto A4571_64](/files/georectify/A4571_64.jpg)
* [1933 Airphoto A4571_65](/files/georectify/A4571_65.jpg)
* [1933 Airphoto A4571_66](/files/georectify/A4571_66.jpg)


### Useful links
* [Map Warper](https://mapwarper.net/)


## Creating a Map Warper account

From the Map Warper homepage, click on ```Create Account``` to [sign up](http://mapwarper.net/u/sign_up) for a free account, then log in. 


## Uploading a map and adding metadata

Choose a map to georectify. I'll be selecting a sheet from the 1901 Fire Insurance Plan of Ottawa for this example. 

Click on the ```Upload Map``` tab, then complete as many metadata fields as you can based on the information you have available. Many fields are optional. I recommend the following:

- **Title:** Sheet 40. Insurance plan of the city of Ottawa, Canada, and adjoining suburbs and lumber districts, January 1888, revised January 1901.
- **Description:** Credit: Library and Archives Canada; Copyright: Expired
- **Tags:** Ottawa
- **Date depicted:** 1901
- **Issue year:** 1901
- **Published:** Charles E. Goad

Locate the file on your computer and then click ```Create``` to upload it. I'm using **227.jpg** as my image for this example.

![Screenshot of the Map Warper uploader screen](/images/upload.jpg)

If the upload is successful, the map you've uploaded will appear on the screen. 

## Choosing ground control points

Choose the ```Rectify``` tab. You'll see two panes -- on the left is the map you'll be rectifying, on the right is a web map. Click on the map in the right pane and zoom in to your target area.

![Screenshot of the Map Warper recifying screen](/images/setup.jpg)

Once you're nicely zoomed in to the same area on both sides, choose the green map marker symbol. Choose an area on your scanned map and click to add a control point. Do the same on the right map to add a control point to the reference map. Once you're happy with your placement, click ```Add Control Point``` at the bottom of the screen. Continue adding matching pairs of control points until they are well-distributed across the scanned map.

![Screenshot of the Map Warper recifying screen](/images/warped.jpg)

Once you have placed several control point pairs, click ```Warp Image!``` to see the scanned map superimposed on the reference map. You can continue to tweak the point placement and warp the map until you are satisfied with the map's alignment.


## Additional features

If your images have borders that are interfering with either the georectification process or the utility of your final webmap, they can be removed with a mask from the ```Crop``` tab.


## Exporting the data

Map Warper offers several options for exporting your georectified images. GeoTIFFs are a common format used in GIS software. KMLs are frequently used in Google Earth. The Tiles option allows the image data to be pulled into several types of web maps, including Leaflet. 

![Screenshot of the Map Warper export screen](/images/export.jpg)

