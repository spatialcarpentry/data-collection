---
title: "Buffer Exercise"
layout: post
category : Get the Data
tagline: 
tags : [analysis, vector, buffer, projections, CRS]
---

{% include JB/setup %}

#### Pre-requisites:

- Setup
- Basics

#### Objecties: 

1. Perform simple spatial function on vector data
2. Further understand projections

#### Exercise: [Buffer Exercise](link)

<!--

#### Data:

iRods access: <br>&nbsp;&nbsp;&nbsp;``/iplant/home/shared/aegis/Spatial-bootcamp/data-collection/buffer-exercise``

1. [Washington state faults - (wa_fault_100k.shp)](http://de.iplantcollaborative.org/dl/d/434DE989-91F4-4A29-BA17-7B08ADF2BFA2/wa_fault_100k.zip) 
-->

----

## Visually explaining map units

Projections can make or break your research- the small things matter the most in spatial data science. This simple exercise will help visually explain projections (in QGIS, coordinate reference systems) and problems you may encounter during your work.

This follow exercise covers a simple spatial function, the Buffer. Spatial functions are explained in later lessons.

 1. Open QGIS and import ``wa_faults_100k.shp`` ![Spatial Data Bootcamp: Vector Analysis - add vector data]({{BASE_PATH}}{{ASSET_PATH}}/images/add-vector.png)<br>**fault_100k.shp**<br>
  <img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/buffer-1.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/buffer-1.png" alt="Spatial Data Bootcamp: Vector Analysis - streams and faults"/>
 1. Buffer fault lines to 100m:
   * <em>Menu Bar > Vector > Geoprocessing Tools > Buffer(s)</em>
   * Configure inputs as follows:<br>**Input vector layer: fault_100k<br>Buffer distance: 100<br>Output shapefile: fault_buffer_100m.shp<br>Add results to canvas: (Checked)<br>Click OK to perform analysis, Close to exit the tool**<br>
 <img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/buffer-2.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/buffer-2.png" alt="Spatial Data Bootcamp: Vector Analysis - buffer analysis"/>
   * <em>Zoom in to a buffer, close enough to see the width</em><br><br><img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/buffer-3.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/buffer-3.png" alt="Spatial Data Bootcamp: QGIS - buffered faults"/><br>
   * <em>Open the meaure tool</em> ![Spatial Data Bootcamp: Vector Analysis - measure tool]({{BASE_PATH}}{{ASSET_PATH}}/images/measure-tool.png)
   * <em>Measure the width of the buffer.</em> Notice how the total width is only about 62 meters, or 200 feet (buffers both sides of line; 100 feet X 2 = 200 feet). Current map units are determined by the CRS, in this case EPSG:2927 is in US feet and we need meters. Simply changing the CRS in Project Properties does not give us the correct results- this is still measured from EPSG:2927 US feet.<br>
   <img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/buffer-4.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/buffer-4.png" alt="Spatial Data Bootcamp: Vector Analysis - measure buffer"/><br><br>**Important:**<br>There are two methods to perfoming a buffer analysis on our shapefile. The problem here is that our CRS is EPSG:2927 (in US feet) and the buffer distance is based on map units (still US feet). The two methods are: convert 100 meters to US feet and use this value in the buffer analysis while maintaining EPSG:2927 (in US feet); OR, reproject the layer thus creating a new file with a CRS in meters, and then reprojecting back to EPSG:2927. We'll go with the former.<br><br>
 1. Now we need to perform the buffer analysis with the correct method. <em>Remove the incorrect buffer layer: fault_buffer_100m.shp</em>
 1. Convert 100 meters to feet... = 328.084 feet.
 1. Again, open the buffer tool: <em>Menu Bar > Vector > Geoprocessing Tools > Buffer(s)</em>
 1. <em>Buffer fault_100k</em> with correct distance:
   * Configure inputs as follow:<br>**Input vector layer: fault_100k<br>Buffer distance: 328<br>Output shapefile: fault_buffer_100m.shp<br>Add result to canvas: (Checked)<br>Click OK to run (overwrite necessary), and CLOSE to exit tool**<br><br>**Reminder:**<br>Buffer distance = 100 meters * 3.28084 feet = 328.084 feet<br> 1 meter = 3.28084 feet<br><br>
   <img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/buffer-5.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/buffer-5.png"  atl="Spatial Data Bootcamp: Vector Analysis - buffer vector"/>
 1. Confirm 100 meter buffer on faults:
   * Open measure tool ![Spatial Data Bootcamp: Vector Analysis - measure tool]({{BASE_PATH}}{{ASSET_PATH}}/images/measure-tool.png) and confirm 200 meter total width (100 meters * 2 = 200 meters)<br>
   <img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/buffer-6.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/buffer-6.png" alt="Spatial Data Bootcamp: Vector Analysis - measure faults buffer"/><br>You've now tackled a large issue related to map units. Move on to the next lesson. No need to save the document or files.

References: 

[^1]: [http://qgis.org](http://www.qgis.org)

[^2]: [http://docs.qgis.org/2.6/en/docs/index.html](http://docs.qgis.org/2.6/en/docs/index.html)

[^3]: [http://www.gdal.org/gdal_rasterize.html](http://www.gdal.org/gdal_rasterize.html)
