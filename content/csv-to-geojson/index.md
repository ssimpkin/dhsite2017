---
title: "CSV to GeoJSON"
weight: 40
---

## Overview

Geographic clues can be hidden in all kinds of documents. In this exercise, we'll collect addresses from the 1890-1891 Ottawa Directory. Library and Archives Canada has digitized [95 microfiche versions of pre-1901 Canadian directories](http://www.bac-lac.gc.ca/eng/discover/directories-collection/Pages/directories-collection.aspx). These are useful resources for researching where people and businesses were located (and the ads are pretty cool too). The following exercise will require a Google account.

![Image of directories](/images/directory.jpg)

### Data files
* [Google Sheet with template](https://docs.google.com/spreadsheets/d/1ClP7IUjAIs50CLtJxRpy8zwd2PDYy0BmyDBGS8Uf00Q/edit?usp=sharing)
* [PDF of the Ottawa Directory from 1890-1891](/files/Directory_1890.pdf)


## Installing the geocoder add-on

If you haven't already, [log into your Google account](https://www.google.ca).

Next, visit the [Geocode by Awesome Table](https://chrome.google.com/webstore/detail/geocode-by-awesome-table/cnhboknahecjdnlkjnlodacdjelippfg?hl=en) page to download the add-on. The Geocode tool links the spreadsheet content to the Google Maps API and allows us to convert address information into geographic coordinates, right in the spreadsheet itself! It also provides some basic mapping functionality.

![Geocoder add-on page](/images/geocoder-download.jpeg)

## Adding data to the table

Make a copy of the [Google Sheets template](https://docs.google.com/spreadsheets/d/1ClP7IUjAIs50CLtJxRpy8zwd2PDYy0BmyDBGS8Uf00Q/edit?usp=sharing) by clicking ```File > Make a copy```.

Next, open the directory PDF and scroll to page 117. You'll see that I've begun transcribing the information from the businesses along the north side of Rideau Street onto the spreadsheet.

Each business is given its own line, and each piece of information about the business is given its own column.

{{< note title="Note" >}}
As you can imagine, modern-day geocoders work best with modern-day address data (we may be pushing it a little). Watch out for renumbered and renamed streets if you attempt this process with historical data. Reference materials such as fire insurance plans can be useful for doing a quality check of historical addresses.
{{< /note >}}

Choose ```Add-ons > Geocode by Awesome Table > Start Geocoding``` to begin. A menu will open on the right side of the screen.

Since the geocoder only looks in one column to find all of the address information, we need to smoosh together the four columns that contain pieces of the address. The add-on will do this for us. Click ```Are your addresses in multiple columns?``` to bring up a second menu. Check *street_address*, *city*, *province*, and *country*, then click ```Insert column```. A new column with the full address will appear.

![Table preview](/images/columns.jpeg)

Next, return to the right side menu. Choose *Sheet1* as the Current sheet and *Full Address* as the Address column. Press ```Geocode!``` and watch as latitude and longitude coordinates appear in new columns.

## Exporting a CSV file

Export the completed table as a CSV file by clicking ```File > Download as > Comma-separated values (.csv, current sheet)```. Save to your computer.

## Previewing with geojson.io

We'll be converting the file from a table to a webmap-friendly format called GeoJSON using a website called [geojson.io](http://geojson.io). The site is a useful way to preview geojson files, trace basic shapes, and convert GeoJSON files to other spatial formats like shapefiles and KMLs.

Drag and drop the CSV file over the map on [geojson.io](http://geojson.io) to import the data.

![geojson.io page with points displayed](/images/geojson.jpeg)

You'll see that points have appeared along Rideau Street. The geocoder took a look at the street addresses and made a best guess about where they might go, based on modern-day data.

You can imagine that the buildings along Rideau Street have likely undergone some major changes since 1890. Fortunately, we can import a reference image to help us quality check the point placements.

Click ```Meta > Add map layer```, then paste in the following URL: ```http://mapwarper.net/maps/tile/20531/{z}/{x}/{y}.png```. Click ```OK```, then enter a layer name (I used *1901*) and click ```OK``` again.

A new overlay will appear showing a fire insurance plan from 1901. Cool, right? We'll be learning how to make these later in the workshop.

![geojson.io page with 1901 map overlay](/images/geojson-overlay.jpeg)

Make any adjustments to the address points (sometimes addresses will be in the centres of modern-day buildings) by clicking on an individual point and the pencil icon on the right side. Using the historical map as a reference, we can have a better idea of how each block looked closer to the time the directory was published.

Once you're happy with the point placement, click ```Save``` next to the pencil icon and then ```Save > GeoJSON``` to export the points as a GeoJSON file.
