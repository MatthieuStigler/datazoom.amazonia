load\_pibmunic
================

Loads information on gross domestic product at current prices, taxes,
net of subsidies, on products at current prices and gross value added at
current prices, total and by economic activity, and respective shares.
Survey is done at Country, state and municipality level and data is
available from 2002 to 2018.

# Usage:

``` r

There are six parameters in this function:
  
  1. dataset: there is only one
 
  # dataset = "pibmunic"
  
  2. raw_data : there are two options:
  
  # TRUE: if you want to visualize the raw data.
  # FALSE: if you want to visualize the processed version of the data. 
  
  3. time_period: data is available from 2002 to 2018
  
  # Ex: time_period = 2002:2004
  
  4. geo_level: there are three options
  
  # "country"
  # "state"
  # "municipality"
  
  5. language : you can choose between portuguese and english
  
  # "pt"
  # "eng"
  
  6. legal_amazon_only: setting the return of Legal Amazon Data (legal_amazon_only = TRUE) or Country´s Data (legal_amazon_only = FALSE)
  
  
```

# Examples:

``` r

# Download raw data (raw_data = TRUE) on gross domestic product (dataset = 'pibmunic') from the entire country (legal_amazon_only = FALSE) by state (geo_level = 'state') during the year 2012 (time_period = 2012) in english (language = "eng").   

 pibmunic <- load_pibmunic(dataset = 'pibmunic',
                           raw_data = TRUE,
                           geo_level = 'state',
                           time_period = 2012,
                           language = "eng",
                           legal_amazon_only = FALSE)

# Download treated data (raw_data = FALSE) on gross domestic product (dataset = 'pibmunic') from the Legal Amazon territory (legal_amazon_only = TRUE) by municipality (geo_level = 'municipality') during the year 2012 (time_period = 2012) in portuguese.   

pibmunic <- load_pibmunic(dataset = 'pibmunic',
                           raw_data = FALSE,
                           geo_level = 'municipality',
                           time_period = 2012,
                           language = "pt",
                           legal_amazon_only = TRUE)
```