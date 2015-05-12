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

#### Data:

iPlant Data Store: <br>&nbsp;&nbsp;&nbsp;``/Community Data/aegis/Spatial-bootcamp/data-collection/buffer-exercise``

1. [data one](link-to-data-one) 

----

## Performing a simple vector spatial function

Projection can make or break your research- the small things matter the most in spatial data scienece. This simple exercise will help visually explain projections (in QGIS, coordinate reference systems) and problems you may encounter during your work.

 1. Open QGIS and configure project workspace.
 1. Import data:
   * HINT: The project projection will default to the first layer that is added to the project (See lower right of image below: EPSG:2927).
   * <em>Add Vector Layer: </em>![Spatial Data Carpentry: Vector Analysis - add vector data]({{BASE_PATH}}{{ASSET_PATH}}/images/add-vector.png)<br>**fault_100k.shp**<br>
   ![Spatial Data Carpentry: Vector Analysis - streams and faults]({{BASE_PATH}}{{ASSET_PATH}}/images/vector-analysis-3.png)
 1. Buffer fault lines to 100m:
   * <em>Menu Bar > Vector > Geoprocessing Tools > Buffer(s)</em>
   * Configure inputs as follows:<br>**Input vector layer: fault_100k<br>Buffer distance: 100<br>Output shapefile: fault_buffer_100m.shp<br>Add results to canvas: (Checked)<br>Click OK to perform analysis, Close to exit the tool**<br>
   ![Spatial Data Carpentry: Vector Analysis - buffer analysis]({{BASE_PATH}}{{ASSET_PATH}}/images/vector-analysis-4.png)
   * <em>Zoom in to a buffer, close enough to see the width</em>
   * <em>Open the meaure tool</em> ![Spatial Data Carpentry: Vector Analysis - measure tool]({{BASE_PATH}}{{ASSET_PATH}}/images/measure-tool.png)
   * <em>Measure the width of the buffer.</em> Notice how the total width is only about 62 meters, or 100 feet. Current map units are determined by the CRS, in this case EPSG:2927 is in US feet and we need meters. Simply changing the CRS in Project Properties does not give us the correct results- this is still measured from EPSG:2927 US feet.<br>
   ![Spatial Data Carpentry: Vector Analysis - measure buffer]({{BASE_PATH}}{{ASSET_PATH}}/images/vector-analysis-measure-tool-2.png)<br><br>**Important:**<br>There are two methods to perfoming a buffer analysis on our shapefile. The problem here is that our CRS is EPSG:2927 (in US feet) and the buffer distance is based on map units (still US feet). The two methods are: convert 100 meters to US feet and use this value in the buffer analysis while maintaining EPSG:2927 (in US feet); OR, reproject the layer thus creating a new file with a CRS in meters (correct map units), and then reprojecting back to EPSG:2927. We'll go with the former.<br><br>
 1. Now we need to perform the buffer analysis with the correct method. <em>Remove the incorrect buffer layer: fault_buffer_100m.shp</em>
 1. <em>Add Vector Layer: </em>![Spatial Data Carpentry: Vector Analysis - add vector]({{BASE_PATH}}{{ASSET_PATH}}/images/add-vector.png)
   * **NHD_MajorStreams.shp<br>**
  ![Spatial Data Carpentry: Vector Analysis - add vector data]({{BASE_PATH}}{{ASSET_PATH}}/images/vector-analysis-5.png)
 1. Open the buffer tool: 
   * <em>Menu Bar > Vector > Geoprocessing Tools > Buffer(s)</em>
 1. <em>Buffer fault_100k:</em>
   * Configure inputs as follow:<br>**Input vector layer: fault_100k<br>Buffer distance: 328<br>Output shapefile: fault_buffer_100m.shp<br>Add result to canvas: (Checked)<br>Click OK to run (overwrite necessary), and CLOSE to exit tool**<br><br>**Reminder:**<br>Buffer distance = 100 meters * 3.28084 feet = 328.084 feet<br> 1 meter = 3.28084 feet<br><br>
   ![Spatial Data Carpentry: Vector Analysis - buffer vector]({{BASE_PATH}}{{ASSET_PATH}}/images/vector-analysis-6.png)
 1. Confirm 100 meter buffer on faults:
   * Open measure tool ![Spatial Data Carpentry: Vector Analysis - measure tool]({{BASE_PATH}}{{ASSET_PATH}}/images/measure-tool.png) and confirm 200 meter total width (100 meters * 2 = 200 meters)<br>
   ![Spatial Data Carpentry: Vector Analysis - measure faults buffer]({{BASE_PATH}}{{ASSET_PATH}}/images/vector-analysis-7.png)
 1. <em>Repeat buffer with NHD_MajorStreams.shp</em>
   * Configure inputs as follows:<br>**Input vector layer: NHD_MajorStreams<br>Buffer distance: 164<br>Output shapefile: streams_buffer_50m.shp<br>Add result to canvas: (Checked)<br>Click OK to run, CLOSE to exit tool**<br><br>**Reminder:**<br>Buffer distance = 50 meters * 3.28084 feet = 164.052 feet<br> 1 meter = 3.28084 feet<br><br>
   ![Spatial Data Carpentry: Vector Analysis - buffer streams]({{BASE_PATH}}{{ASSET_PATH}}/images/vector-analysis-8.png)
 1. Confirm 50 meter buffer on streams.


References: 

[^1]: [http://qgis.org](http://www.qgis.org)

[^2]: [http://docs.qgis.org/2.6/en/docs/index.html](http://docs.qgis.org/2.6/en/docs/index.html)

[^3]: [http://www.gdal.org/gdal_rasterize.html](http://www.gdal.org/gdal_rasterize.html)
