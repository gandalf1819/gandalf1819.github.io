---
layout: post
title: "Risk Factor Identification using Truck Fleet Data"
tags: [ ETL ]
featured_image_thumbnail: assets/images/truck-fleet.jpg
featured_image: assets/images/truck-fleet.jpg
---

![](/assets/images/truck-fleet.jpg)

## Risk Factor Identification using Truck Fleet Data

* This usecase is to analyse various parameters of truck fleet
* Each truck has been equipped to log location and event data
* These events are streamed back to a datacenter where the data will be processed
* The company wants to use this data to understand the risk

### Data 

* Collected geo-location and truck data has been provided
* Size of the truck data is small which can be stored in RDBMS - which will be imported into Sqoop
* Geo-location data will be stored in HDFS

### Architecture

![](/assets/images/truckfleet-architecture.png)

### Steps 

* Load the captured sensor data into Hadoop (HDFS)
* Load truck data from RDBMS to HDFS/Hive
* Run Hive, Pig scripts that compute truck mileage and driver risk factor
* Access the refined sensor data with Microsoft Excel
* Visualize the sensor data using Excel Power View / Pivot Table /Graphs

### Loading data into Hive

![](/assets/images/load-data-1.png)

### Analysing Data

The business objective is to better understand the risk the company is under from fatigue of drivers, over-used trucks, and the impact of various trucking events on risk

![](assets/images/load-data-2.png)

Check the code for the project here: [TruckRisk](https://github.com/gandalf1819/Risk-Factor-Identification-using-Truck-Fleet-Sensor-Data)