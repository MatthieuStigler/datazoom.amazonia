
<!-- README.md is generated from README.Rmd. Please edit that file -->

# datazoom.amazonia

<!-- badges: start -->

[![R build
status](https://github.com/datazoompuc/datazoom.amazonia/workflows/R-CMD-check/badge.svg)](https://github.com/datazoompuc/datazoom.amazonia/actions)

<!-- badges: end -->

\[EDIT THIS\]

The goal of datazoom.amazonia is to facilitate access to official data
regarding the Amazon. The package provides functions that download and
pre-process selected datasets. Data is in general provided at the
municipality-year level (see the documentation for more information).

## Installation

Currently you can only install the development version from
[GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("datazoompuc/datazoom.amazonia")
```

# 1\) INPE data:

## 1.1) PRODES:

Loads information on clearcut deforestation in the Legal Amazon and
annual deforestation rates in the region. Survey is done at state or
municipality level and data is available from 2000 to 2020.

``` r
There are five parameters in this function:
  
  1. dataset = "prodes"
 
  2.raw_data : there are two options:
  # TRUE: if you want to visualize the raw data.
  # FALSE: if you want to visualize the processed version of the data. 
 
  3. geo_level: you can choose between "state" and "municipality"
  
  4. time_period : available from 2000 to 2020
  
  5. language : you can choose between portuguese and english
  
Examples:

# Download raw data (raw_data = TRUE) by municipality (geo_level = "municipality") from 2000 to 2005 (time_period = 2000:2005) in english.

data = load_prodes(dataset = "prodes", raw_data = TRUE,
                        geo_level = "municipality", time_period = 2000:2005,
                        language = 'eng') 

# Download treated data (raw_data = FALSE) by state (geo_level = "state") from 2010 (time_period = 2010) in portuguese (language = 'pt').

data = load_prodes(dataset = "prodes", raw_data = FALSE,
                        geo_level = "state", time_period = 2010,
                        language = 'pt') 
```

## 1.2) DETER:

Loads information on change in forest cover in the Amazon. Survey is
done at state or municipal level.

``` r
There are five parameters in this function:
  
  1. dataset: there are two options:
  # information about Amazon:   dataset = "deter_amz" 
  # information about Cerrado:  dataset =  "deter_cerrado"
  
  2.raw_data: there are two options:
  # TRUE: if you want to visualize the raw data.
  # FALSE: if you want to visualize the processed version of the data. 
  
  3. geo_level: you can choose between "state" and "municipality"
  
  4. time_period : you can choose from 1988 to 2020

  5. language : you can choose between portuguese and english


Examples:

# Download raw data (raw_data = TRUE) about Amazon (dataset = "deter_amz") by state (geo_level = "state") from 1988 to 1990 (time_period = 1988:1990) in english (language = 'eng')

data = load_deter(dataset = "deter_amz" , raw_data = TRUE,
                       geo_level = "state", time_period = 1988:1990,
                       language = 'eng') 

# Download treated data (raw_data = FALSE) about Cerrado (dataset = "deter_cerrado") by municipality (geo_level = "municipality") from 2010 (time_period = 2010) in portuguese (language = 'pt')

data = load_deter(dataset = "deter_cerrado" , raw_data = FALSE,
                       geo_level = "municipality", time_period = 2010,
                       language = 'pt')
  
```

## 1.3) DEGRAD:

Loads information on forest degradation in the Brazilian Amazon,
replaced by DETER-B in December 2016. Data is available from 2007 to
2016.

``` r
There are four parameters in this function:
  
  1. dataset = "degrad"

  2.raw_data : there are two options:
  # TRUE: if you want to visualize the raw data.
  # FALSE: if you want to visualize the processed version of the data. 
  
  3. time_period : data is available from 2007 to 2016

  4. language : you can choose between portuguese and english
  
Examples:
  
# download raw data (raw_data = TRUE) related to forest degradation from 2010 to 2012 (time_period = 2010:2012) in portuguese (language = "pt"): 

data = load_degrad(dataset = 'degrad', raw_data = TRUE,
                        time_period = 2010:2012,
                        language = 'pt')

# download treated data (raw_data = FALSE) related to forest degradation from 2013 (time_period = 2013) in english (language = "eng"): 

data = load_degrad(dataset = 'degrad', raw_data = FALSE,
                        time_period = 2013,
                        language = 'eng')
```

# 2\) COMEX data:

The Comex dataset gathers data extracted from Siscomex (Integrated
System of Foreign Trade), which is a database containing information
from all products that are imported to or exported from Brazil. Using
data reported from the companies which are responsible for the process
of transporting the products, the system adheres to internationally
standardized nomenclatures, such as the Harmonized System and the
Mercosul Common Nomenclature (which pertains to members of the Mercosul
organization).

The data has a monthly frequency and is available starting from the year
1989. From 1989 to 1996, a different system of nomenclatures was
adopted, but all conversions are available on a dictionary in the Comex
website (<http://www.mdic.gov.br/balanca/bd/tabelas/NBM_NCM.csv>).

``` r

There are five parameters in this function:
  
  1. dataset: there are three choices:
  # "comex_export_mun" : selects exports data by municipality
  # "comex_import_mun" : selects imports data by municipality
  # "comex_export_prod" :
  # "comex_import_prod" :
  
  2.raw_data : there are two options:
  # TRUE: if you want to visualize the raw data.
  # FALSE: if you want to visualize the processed version of the data. 
  
 3. time_period : available starting from the year 1989

 4. language : you can choose between portuguese and english
 
 5. prod_class: A string indicating the classification to be downloaded. There are four possibilities:
 
 # "hs"   : (SH - Sistema Harmonizado/Harmonized System) - this is an international system that classifies products. It was created by the World Customs Organization (Organização Mundial das Alfândegas)
 
 # "cuci" : (CUCI - Classificação Uniforme do Comércio Internacional/ Standard International Trade Classification). It is based on the type of material utilised during the production, the stage of the production process, the importance of the product in international trade and the tecnology used. 
 
 # "isic" : (ISIC - Classificação Internacional Padrão por Atividade Econômica/ International Standard Industrial Classification). According to the United Nations: the scope of ISIC in general covers productive activities, i.e., economic activities within the production boundary of the System of National Accounts (SNA). A few exceptions have been made to allow for the classification of activities beyond the production boundary but which are of importance for various other types of statistics. These economic activities are subdivided in a hierarchical, four-level structure of mutually exclusive categories, facilitating data collection, presentation and analysis at detailed levels of the economy in an internationally comparable, standardized way. The categories at the highest level are called sections, which are alphabetically coded categories intended to facilitate economic analysis. The sections subdivide the entire spectrum of productive activities into broad groupings, such as “Agriculture, forestry and fishing”, “Manufacturing” and “Information and communication”.The classification is then organized into successively more detailed categories, which are numerically coded: two-digit divisions; three-digit groups; and, at the greatest level of detail, four-digit classes. 
 
 # "cgce" : (CGCE - Classificação por Grandes Categorias Econômicas/Broad Economic Categories). Organizes data of the international trade in large groups following the classification of CUCI (Standard International Trade Classification).


   
Examples:
   
# download treated (raw_data = FALSE) exports data by municipality (dataset = "comex_export_mun") from 1997 to 2021 (time_period = 1997:2021) following the "hs" classification (prod_class = "hs")

data = load_br_trade(dataset = "comex_export_mun", 
                         raw_data = FALSE, time_period = 1997:2021, prod_class = "hs")

# download treated(raw_data = FALSE) imports data by municipality (dataset = "comex_import_mun") from 1997 to 2021 (time_period = 1997:2021) using "CUCI" classification (prod_class = "cuci")
 
data = load_br_trade(dataset = "comex_import_mun",
                               raw_data = FALSE, time_period = 1997:2021,
                               prod_class = "cuci")
```

# 3\) IBGE data:

## 3.1) PIB-Munic:

Loads information on gross domestic product at current prices, taxes,
net of subsidies, on products at current prices and gross value added at
current prices, total and by economic activity, and respective shares.
Survey is done at Country, state and municipality level and data is
available from 2002 to 2018.

``` r

There are six parameters in this function:
  
  1. dataset = "pibmunic"
  
  2. raw_data : there are two options:
  # TRUE: if you want to visualize the raw data.
  # FALSE: if you want to visualize the processed version of the data. 
  
  3. time_period: data is available from 2002 to 2018
  
  4. geo_level: there are three options
  # "country"
  # "state"
  # "municipality"
  
  5. language : you can choose between portuguese and english
  
  6. legal_amazon_only: setting the return of Legal Amazon Data (legal_amazon_only = TRUE) or Country´s Data (legal_amazon_only = FALSE)
  

Examples:
  
# Download raw data (raw_data = TRUE) on gross domestic product (dataset = 'pibmunic') from the entire country (legal_amazon_only = FALSE) by state (geo_level = 'state') from 2012 (time_period = 2012) in english (language = "eng").   

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

## 3.2) CEMPRE:

Loads information on companies and other organizations and their
respective formally constituted local units, registered with the CNPJ -
National Register of Legal Entities. Data is available from 2006 to
2019.

``` r

There are seven parameters in this function:
  
  1. dataset = "cempre"
 
  2. raw_data : there are two options:
  # TRUE: if you want to visualize the raw data.
  # FALSE: if you want to visualize the processed version of the data.

  3. geo_level: "country", "state" or "municipality"
  
  4. time_period: data is available from 2006 to 2019

  5. language : you can choose between portuguese and english
 
  6. sectors: defines if the data will be return separated by sectors (sectors = TRUE) or not (sectors = FALSE)

  7. legal_amazon_only: setting the return of Legal Amazon Data (legal_amazon_only = TRUE) or Country´s Data (legal_amazon_only = FALSE). You should know that legal_amazon_only = TRUE is only available for geo_level = "municipality".
  
Examples: 
  
# Download raw data (raw_data = TRUE) with the aggregation level being the country ( geo_level = "country") from 2008 to 2010 (time_period = 2008:2010) in english (language = "eng"). In this example, the user did not want to visualize data by sector (sectors = FALSE) and the user also wanted the data to be restricted to the  Legal Amazon area (legal_amazon_only = TRUE).

data = load_cempre(dataset = "cempre", raw_data = TRUE,
                        geo_level = "country", time_period = 2008:2010,
                        language = "eng", sectors = FALSE,
                        legal_amazon_only = TRUE) 

# Download treated data (raw_data = FALSE) by state ( geo_level = "state") from 2008 to 2010 (time_period = 2008:2010) in portuguese (language = "pt"). In this example, the user wanted to visualize data by sector (sectors = TRUE) and the user also did not want the data to be restricted to the  Legal Amazon area (legal_amazon_only = FALSE)


data = load_cempre(dataset = "cempre", raw_data = FALSE,
                        geo_level = "state", time_period = 2008:2010,
                        language = "pt", sectors = TRUE,
                        legal_amazon_only = FALSE) 
```

## 3.3) SIGMINE:

Loads information the mines being explored legally in Brazil, including
their location, status, product being mined and area in square meters
etc. Survey is done at municipal and state level. The National Mining
Agency (ANM) is responsible for this survey.

``` r
There are four parameters in this function:
  
  1. dataset = 'sigmine_active'

  2. raw_data: there are two options:
  # TRUE: if you want to visualize raw data.
  # FALSE: if you want to visualize processed data. 

  3. geo_level: "municipality" or "state"
  
  4. language : you can choose between portuguese and english
  
 
Examples:

# Download raw data (raw_data = TRUE) by municipality (geo_level = "municipality") in english (language = 'eng').

data = load_sigmine(dataset = 'sigmine_active',
                        raw_data = TRUE, geo_level = "municipality",
                        language = 'eng')

# Download treated data (raw_data = FALSE) by state (geo_level = "state") in portuguese (language = 'pt')

data = load_sigmine(dataset = 'sigmine_active',
                        raw_data = FALSE, geo_level = "state",
                        language = 'pt')
```

## 3.4) PAM:

Municipal Agricultural Production (PAM, in Portuguese) is a nationwide
annual survey conducted by IBGE (Brazilian Institute of Geography and
Statistics) which provides information on agricultural products, such as
quantity produced, area planted and harvested, average quantity of
output and monetary value of such output. The products are divided in
permanent and temporary farmed land, as well as dedicated surveys to the
four products that yield multiple harvests a year (beans, potato, peanut
and corn), which all sum to a total survey of 64 agricultural products
(31 of temporary tillage and 33 of permanent tillage). Output, however,
is only included in the dataset if the planted area occupies over 1 acre
or if output exceeds one tonne.

``` r
There are five parameters in this function:
  
  1. dataset: There are seven possible choices. 

  These datasets contain statistics such as quantity produced, area planted and harvested, average quantity of output and monetary value of such output. 
  
  # 'pam_all_crops' : it selects data about agricultural products divided in permanent and temporary farmed land. 
  # 'pam_permanent_crops' : it selects the data about agricultural products produced in permanent farmed land.
  # 'pam_temporary_crops' :it selects the data about agricultural products produced in temporary farmed land.
  # 'pam_corn' : it selects the data from the first and the second harvests of corn.
  # 'pam_potato' : it selects the data from the first, the second and the third harvests of potato.
  # 'pam_peanut' : it selects the data from the first and the second harvests of peanut.
  # 'pam_beans' :  it selects the data from the first, the second and the third harvests of bean.

  2. raw_data: there are two options:
  
  # TRUE: if you want to visualize the  data as it is in the IBGE's site.
  # FALSE: if you want to visualize the treated (more organized) version of the data. 

  3. geo_level: there are four options:
  
  # "country"
  # "region"
  # "state" 
  # "municipality"

  4. time_period:
    
  # For pam_all_crops, pam_permanent_crops and pam_temporary_crops, data is available from 1974 to 2019.
  # For pam_corn, pam_potato, pam_peanut and pam_beans, data is avaiable from 2003 to 2019.
    
  5. language : you can choose between portuguese and english
  

Examples:

# Download treated (raw_data = FALSE) data related to the production from permanent and temporary farmed lands (dataset = 'pam_all_crops') by state (geo_level = "state") from 1980 to 1990 (time_period = 1980:1990) in english (language = "eng").

data = load_pam(dataset = 'pam_all_crops', raw_data = FALSE, geo_level = "state", time_period = 1980:1990, language = "eng")

# Download raw data (raw_data = TRUE) related to the corn production (dataset = 'pam_corn') by municipality (geo_level = "municipality") from 2010 to 2012 (time_period = 2010:2012) in portuguese (language = "pt").

data = load_pam(dataset = 'pam_corn', raw_data = TRUE, geo_level = "municipality", time_period = 2010:2012, language = "pt")
```

## 3.5) PEVS:

Loads information on the amount and value of the production of the
exploitation of native plant resources and planted forest massifs, as
well as existing total and harvested areas of forest crops. Survey is
done at the municipal level and data is available from 1986 to 2019.

``` r

There are five parameters in this function:
  
  1. dataset: there are three choices:
  # 'pevs_forest_crops' : provides data related to both quantity and value of the forestry activities. The data goes from 1986 to 2019 and it is divided by type of product.
  # 'pevs_silviculture' : provides data related to both quantity and value of the silviculture. The data goes from 1986 to 2019 and it is divided by type of product.
  # 'pevs_silviculture_area' : total existing area used for silviculture in 12/31.The data goes from 2013 to 2019 and it is divided by forestry species.  
  
  2.raw_data : there are two options:
  # TRUE: if you want to visualize the  data as it is in the IBGE's site.
  # FALSE: if you want to visualize the treated (more organized) version of the data. 
  
  3. geo_level : there are four options:
  
  # "country"
  # "region"
  # "state"
  # "municipality"
  
  4. time_period : data goes from 1986 to 2019, except for the pevs_silviculture_area dataset where data is available from 2013 to 2019.

  5. language : you can choose between portuguese and english
 
Examples:
  
# Download treated (raw_data = FALSE) silviculture data (dataset = 'pevs_silviculture') by state (geo_level = 'state') from 2012 (time_period =  2012) in portuguese (language = "pt")

data = load_pevs(dataset = 'pevs_silviculture', raw_data = FALSE ,geo_level = 'state', time_period =  2012, language = "pt")

# Download raw (raw_data = TRUE) forest crops data (dataset = 'pevs_forest_crops') by municipality (geo_level = 'municipality') from 2012 to 2013 (time_period =  2012:2013) in english (language = "eng")

data = load_pevs(dataset = 'pevs_forest_crops', raw_data = TRUE, geo_level = "municipality", time_period = 2012:2013, language = "eng")
```

## 3.6) PPM:

Downloads data from PPM (“Pesquisa da Pecuária Municipal”). This survey
contains information of the livestock inventories (e.g:cattle, pigs and
hogs) in Brazilian Municipalities. It also provides information on the
production of animal origin (e.g:output of milk, hen eggs, quail eggs,
honey) and the value of the production during the reference year.

The periodicity of the survey is annual. The geographic coverage is
national, with results released for Brazil, Major Regions, Federation
Units, Mesoregions, Microregions and Municipalities.

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

  3. geo_level: there are four options:
  # "country"
  # "region"
  # "state"
  # "municipality"
    
  4. time_period:
  
  # For ppm_livetock_inventory, ppm_sheep_farming, ppm_animal_orig_production and ppm_cow_farming: data is avaiable from 1974 to 2019.
  # For ppm_aquaculture: data is avaiable from 2013 to 2019 
  
  5. language : you can choose between portuguese and english
  

Examples:
  
   # Download treated data (raw_data = FALSE) about aquaculture (dataset = 'ppm_aquaculture') from 2013 to 2015 (time_period = 2013:2015) in english (language = "eng") with the level of aggregation being the country (geo_level = "country"). 

data = load_ppm(dataset = 'ppm_aquaculture', raw_data = FALSE, geo_level = "country", time_period = 2013:2015, language = "eng")

# Download raw data (raw_data = TRUE) about sheep farming (dataset = 'ppm_sheep_farming') by state (geo_level = "state") from 1980 to 1995 (time_period = 1980:1995) in portuguese (language = "pt")

data = load_ppm(dataset = 'ppm_sheep_farming', raw_data = TRUE, geo_level = "state", time_period = 1980:1995, language = "pt")
```

# 4\) IPS:

Loads information on the social and environmental performance of the
Legal Amazon. Survey is done at the municipal level and data is
available in 2014 and 2018.

``` r
There are four parameters in this function:
  
  1. dataset = "ips"

  2.raw_data : there are two options:
  # TRUE: if you want to visualize the raw data.
  # FALSE: if you want to visualize the processed version of the data. 
  
  3. time_period : data is available in 2014 and 2018.

  4. language : you can choose between portuguese and english
  
Examples:

# Download raw data (raw_data = TRUE) from 2014 (time_period = 2014) in english (language = 'eng')

data = load_ips(dataset = "ips", raw_data = TRUE,
                    time_period = 2014, language = 'eng')

# Download treated data (raw_data = FALSE) from 2014 (time_period = 2018) in portuguese (language = 'pt')

data = load_ips(dataset = "ips", raw_data = FALSE,
                    time_period = 2018, language = 'pt')
```

# 5\) SEEG:

Loads data of estimates of emission of greenhouse gases of Brazilian
cities.

According to the “SEEG Brasil” website: all five sectors that are
sources of emissions - Agriculture, Energy, Land Use Change, Industrial
Processes and Waste with the same degree of detail contained in the
emissions inventories are evaluated. The data provided in SEEG’s
Collection 8 is a series covering the period from 1970 to 2019, except
for the Land Use Change Sector that has the series from 1990 to 2019.

``` r

There are four parameters in this function:
  
  1. dataset = "seeg"
  
  2. raw_data: there are two options:
  # TRUE: if you want to visualize the raw data.
  # FALSE: if you want to visualize the processed version of the data. 
  
  3. geo_level: there are three options:
  # "country" 
  # "state"  
  # "municipality"
  
   5. language : you can choose between portuguese and english
  
Examples:

# Download raw data (raw_data = TRUE) of greenhouse gases (dataset = "seeg") by municipality (geo_level = "municipality") in english (language = "eng")

data = load_seeg(dataset = "seeg", raw_data = TRUE,
                      geo_level = "municipality", language = "eng")
  

# Download processed data (raw_data = FALSE) of greenhouse gases (dataset = "seeg") by state (geo_level = "state") in portuguese (language = "pt")
  
data = load_seeg(dataset = "seeg", raw_data = FALSE,
                      geo_level = "state", language = "pt")
```

# 6\) IBAMA:

Downloads and compiles data on environmental fines at the municipality
or state levels considering the Amazon region. The user has the option
to either download or load the previously stored raw data, choosing a
time-location aggregation level.

The function returns a data frame with aggregates considering, for each
time-location period, counts for total the number of infractions,
infractions that already went to trial, and number of unique
perpetrators of infractions.

``` r

There are five parameters in this function:

  1. dataset = "areas_embargadas"
  
  2. raw_data : there are two options:
  # TRUE: if you want to visualize the raw data.
  # FALSE: if you want to visualize the processed version of the data. 
 
  3. geo_level: "municipality" or "state"
  
  4. language : you can choose between portuguese and english
  
  5. legal_amazon_only: setting the return of Legal Amazon Data (legal_amazon_only = TRUE) or Country´s Data (legal_amazon_only = FALSE)
  
Examples:

# Download treated data (raw_data = FALSE) by municipality (geo_level = "municipality") from the entire country (legal_amazon_only = FALSE) in english (language = "eng")
  
data = load_ibama(dataset = "areas_embargadas", raw_data = FALSE, 
                  geo_level = "municipality", language = "eng",
                  legal_amazon_only = FALSE)

# Download raw data (raw_data = TRUE) by state (geo_level = "state") from Legal Amazon region (legal_amazon_only = TRUE) in portuguese (language = "pt")
  
data = load_ibama(dataset = "areas_embargadas", raw_data = TRUE, 
                  geo_level = "state", language = "pt",
                  legal_amazon_only = TRUE)
```

## Credits

DataZoom is developed by a team at Pontifícia Universidade Católica do
Rio de Janeiro (PUC-Rio), Department of Economics. Our official website
is at: <http://www.econ.puc-rio.br/datazoom>.