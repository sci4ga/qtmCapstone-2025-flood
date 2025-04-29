# QTMCapstone-2025-flood

**Discover Land Cover and Flooding in Georgia**
***Summer Sun, Sylvia Xing, Ellie Yang***
## Overview of the Project
The project “Discover Land Cover and Flooding in Georgia” is a data story constructed during the Emory QTM Capstone class. The project is planned to explore the connection between land cover change and flooding events in Georgia, and thus raise awareness among community members about flooding. Mainland cover types looked into are forest, wetland, and developed sites. This shared folder contains all the datasets and their descriptions for this project.
**Link to Data Story:** https://arcg.is/zmm1q2


## Land Cover Analysis

https://github.com/sci4ga/qtmCapstone-2025-flood/blob/main/Land_Cover_Code.zip

**Packages and python version:**  

Python 3.11.5 

Packages used: pandas, os, glob, matplotlib.pyplot, sklearn.linear_model 

The raw data on the National Land Cover Database(NLCD) were 159 CSV files, each containing the land cover data from 1985-2023 for all the counties (159 in total) in Georgia. The data has two versions:  
1. the unit is in square kilometer  
2. the unit is the percentage of this land cover type in the county.  

**Combline_ALL_km:** Combine all 159 csv files (km^2 unit) in a single csv  

**NLCD_change_rate_km:** calculate the change rate of land covers for all counties using formula: (End year - Start year)/Start year  

**roc_process_percentage:** Combine all 159 csv files (percentage unit) in a single csv then calculate  the change rate of land covers for all counties using formula: [(End year - Start year)/Start year]*100  

*Note that some land covers (e.g.emergent herbaceous wetlands and woody wetlands) are combined to a single type (e.g. wetlands) for analysis; the combination can be found in the type_map in both rate of change calculation file*  

**Visualization and merge shapes_km:** Make a preliminary visualization by coloring each county with its most prominent land cover type; then merge the NLCD dataset (km^2 unit) with the shpefile of Georgia counties for making maps on ESRI  

**Visualization_ESRI_percentage:** Merge the NLCD dataset (percentage unit) with the shpefile of Georgia counties for making maps on ESRI  

**regression and land cover analyses:** Including following contents:  
- Make 3 regressions, with x being the percentage mean coverage of wetland, forest or developed sites in 2018-2023, and y being the storm event account in 2018-2023;  
- Area change of wetland, forest, and developed sites from 1985-2023;  
- Percentage change of wetland, forest, and developed sites from 2000-2023;  
- Plot in the year when developed sites increased most, which kinds of land decreased most;  
- Rank of all kinds of land covers in its percentage change from 2000 in descending order.  


## Data Cleaning Updated  
https://github.com/sci4ga/qtmCapstone-2025-flood/blob/main/data%20clean%20updated.ipynb

**Packages and python version:**

Python 3.11.5 

Packages used: pandas, numpy, folium, re, mpl_toolkits.basemap, seaborn, os, glob, matplotlib.pyplot

- A data cleaning file of CSVs that records flood event details from 1985 to 2024, merged with location files, with folium maps created by year and month, giving an overview of how flood events are distributed


## Storm-Event Rate-of-Change (RoC) Analysis  
https://github.com/sci4ga/qtmCapstone-2025-flood/blob/main/StormData%20RoC%20Cla.ipynb

***A county-level look at how Georgia flood events have changed from 2000-2005 to 2018-2023***

### Overview
**Packages and python version:**

Python 3.11.5 

Packages used: pandas, numpy, seaborn, re, geopandas, shapely.geometry, os, glob, matplotlib.pyplot

`StormData RoC Cla.ipynb` merges **NOAA Storm Events** detail, location and
fatality CSVs for 2000-2023, cleans and joins them with county polygons.

- The original dataset is large, including data from all states in the US and different kinds of events (e.g., flood, hurricane, thunderstorm, etc.).
  
- We are selecting only data from 2000-2024, as data before 1996 are either not significant enough or do not specify a majority of counties in Georgia, which brings trouble to the merging process.
  
- Events from Georgia are selected. Among the events, only `Flood`, `Flash Flood`, and `Coastal Flood` are selected to be considered. According to suggestion, ‘Hurricane’ will be taken into consideration in the future.
   
- Merging with the Location files of each corresponding year based on the (`EVENT_ID`)
  
- Each row contains (`EVENT_ID`) (specify the event), state/county, and begin/end time of each flood event, as well as the location information (coordinates) of each event.
  
- Thus, we can utilize the folium map to visualize the distribution of flood events that happened in Georgia for each year/month.
  
- We utilized the data from 1996 and 2024 to calculate the rate of change of the flood events that occurred in each county. We have counted the number of the floods of the two years and calculated the percentage changes of the numbers, taken as the rate of change of the flood event:

- Aggregate yearly event counts (`event_count`) and total flood-duration (minutes) by county (`CZ_NAME`).

- Total flood-duration is calculated by (`END_TIME`) -  (`BEGIN_TIME`)

- Compares two multi-year windows (2000-2005 vs 2018-2023) and computes  
   `rate_change_percent` for both event counts and duration (minutes) per county per year.
   
- Normalized rate of change calculation by setting the range from -100 to 100.

- Exports tidy CSV summaries and GeoJSONs for future heatmap and swipe map creation:
     - rate_change_per_county_Storm.csv https://github.com/sci4ga/qtmCapstone-2025-flood/blob/main/rate_change_per_county_Storm.csv 
     - 0023_Normalized_event_count_comparison_RoC 1.csv https://github.com/sci4ga/qtmCapstone-2025-flood/blob/main/0023_Normalized_event_count_comparison_RoC%201.csv
     - merged_details (1).geojson https://github.com/sci4ga/qtmCapstone-2025 flood/blob/main/merged_details(1).geojson

- Generates Visualizations for event count distribution by years, as well as limitations of the duration data in the database.


—


