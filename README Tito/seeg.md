load\_seeg
================

Loads data of estimates of emission of greenhouse gases of Brazilian
cities.

According to the “SEEG Brasil” website: all five sectors that are
sources of emissions - Agriculture, Energy, Land Use Change, Industrial
Processes and Waste with the same degree of detail contained in the
emissions inventories are evaluated. The data provided in SEEG’s
Collection 8 is a series covering the period from 1970 to 2019, except
for the Land Use Change Sector that has the series from 1990 to 2019.

# Usage:

``` r

There are four parameters in this function:
  
  1. dataset: it has only one option:
  
  # dataset = "seeg"
  
  2. raw_data: there are two options:
  
  # TRUE: if you want to visualize the raw data.
  # FALSE: if you want to visualize the processed version of the data. 
  
  3. geo_level: there are three options:
  
  # "country" 
  # "state"  
  # "municipality"
  
   5. language : you can choose between portuguese and english
  
  # "pt"
  # "eng"
```

# Examples:

``` r

# Download raw data (raw_data = TRUE) of greenhouse gases (dataset = "seeg") by municipality (geo_level = "municipality") in english (language = "eng")

load_seeg <- function(dataset = "seeg", raw_data = TRUE,
                      geo_level = "municipality", language = "eng")
  

# Download processed data (raw_data = FALSE) of greenhouse gases (dataset = "seeg") by state (geo_level = "state") in portuguese (language = "pt")
  
oad_seeg <- function(dataset = "seeg", raw_data = FALSE,
                      geo_level = "state", language = "pt")
 
```