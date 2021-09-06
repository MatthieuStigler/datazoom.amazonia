load\_ppm
================

Downloads data from PPM (“Pesquisa da Pecuária Municipal”). This survey
contains information of the livestock inventories (e.g:cattle, pigs and
hogs) in Brazilian Municipalities. It also provides information on the
production of animal origin (e.g:output of milk, hen eggs, quail eggs,
honey) and the value of the production during the reference year.

The periodicity of the survey is annual. The geographic coverage is
national, with results released for Brazil, Major Regions, Federation
Units, Mesoregions, Microregions and Municipalities.

# Usage

``` r
There are five parameters in this function:
  
  1. dataset: There are five possible choices. 

  # 'ppm_livetock_inventory'
  # 'ppm_sheep_farming'
  # 'ppm_animal_orig_production' 
  # 'ppm_cow_farming'
  # 'ppm_aquaculture' 

  2. raw_data: there are two options:
  
  # TRUE: if you want to visualize the  data as it is in the IBGE's site.
  # FALSE: if you want to visualize the treated (more organized) version of the data. 

  3. geo_level: there are six options:
  
  # "country"
  # "region"
  # "state"
  # "mesoregion"
  # "microregion"
  # "city"
  
  4. time_period:
  
  # For ppm_livetock_inventory, ppm_sheep_farming, ppm_animal_orig_production and ppm_cow_farming: data is avaiable from 1974 to 2019.
  # For ppm_aquaculture: data is avaiable from 2013 to 2019 
  
  5. language : you can choose between portuguese and english
  
  # "pt"
  # "eng"

    
```

# Examples

``` r

# Download treated data (raw_data = FALSE) about aquaculture (dataset = 'ppm_aquaculture') by mesoregion (geo_level = "mesoregion") from 2013 to 2015 (time_period = 2013:2015) in english (language = "eng")

data = load_ppm(dataset = 'ppm_aquaculture', raw_data = FALSE, geo_level = "mesoregion", time_period = 2013:2015, language = "eng")

# Download raw data (raw_data = TRUE) about sheep farming (dataset = 'ppm_sheep_farming') by state (geo_level = "state") from 1980 to 1995 (time_period = 1980:1995) in portuguese (language = "pt")

data = load_ppm(dataset = 'ppm_sheep_farming', raw_data = TRUE, geo_level = "state", time_period = 1980:1995, language = "pt")
```