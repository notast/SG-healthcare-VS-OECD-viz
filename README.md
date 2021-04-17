# Background 
The current Singapore healthcare landscape is painted in a storyboard against OECD and non-OECD peers and addresses if Singapore needs to scale up its healthcare resources to ride the silver tsunami. 

## Software 
Storyboard was done in [`Tableau`](https://public.tableau.com/profile/notast#!/vizhome/SingaporevsOECDhealtcareresources/Storyboard). [Data preparation was done in `R`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/health%20exp%20%26%20resource.Rmd) with `tidyverse`, `rvest`, `countrycode`. 

# Data
There are two datasets. The primary dataset has 1230 rows and 13 columns. The primary dataset consists of data from various sources. Variables from various sources were matched as close as possible based on available meta-data. The secondary dataset has 18 rows and 5 columns. It consists of aggerated values from the primary dataset. 

## Multiple Sources
Rudimentary, healthcare provision includes the number of beds, doctors and nurses a country has. Nonetheless, it will be myopic to operate healthcare on a unilateral plane, healthcare needs to be treated as a multi-disciplinary field for more optimal provision. Thus, additional data such as demography (e.g. the proportion elderly population `pct_Elder`) and economic status (e.g. healthcare spending expressed as share of GDP `pct_GDP` and income status of the country `Income_group`) were included. 

The multiple sources are from international organizations (e.g. Organisation for Economic Co-operation and Development and World Bank) and national organizations (e.g. Government of Singapore’s data repository, data.gov.sg, and its department of statistics). 

## Data dictionary 
### Primary dataset [`df_all`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/df_all.csv)
|     #     |     Variable     |     Meaning     |
|-|-|-|
|     1    |     Country     |     40   countries   including Singapore.   Country names were standardized to the names used in [`R`’s `countrycode`   package](https://vincentarelbundock.github.io/countrycode/)      |
|     2    |     Year     |     2008-2017.   An   attempt was made to use the most   up to date data but data after 2017 from     some sources were not available. A decade’s worth of data was used to   reveal   any trends.    |
|     3    |     Resource    |      There are     three types of `resource`s per year and country as dataset is in a   long tidy   format. <br> `Bed`   refers   to beds for acute care,   psychiatric care, rehabilitation, long term care   (e.g. nursing homes) and other care needs   (e.g. palliative). [Source for OECD     and non-OECD countries]( https://data.oecd.org/healtheqt/hospital-beds.htm)   available on GitHub as   [`OECD_beds`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/OECD_beds.csv).[Source   for Singapore](   https://www.tablebuilder.singstat.gov.sg/publicfacing/createDataTable.action?refId=15276)   available on GitHub as [`SG_bed(abs num)`](   https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/SG_bed(abs%20num).csv).   <br> `Dr` refers to   doctors.   [Source for OECD and non-OECD countries]( https://data.oecd.org/healthres/doctors.htm)   available on GitHub as   [`OECD_Drs`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/OECD_Drs.csv).    [Source for Singapore](   https://data.gov.sg/dataset/healthcare-professional-to-population-ratio)   available on GitHub as [`SG_DrsNurses`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/SG_DrsNurses.csv).   <br> `Nurse` refers   to   nurses.[Source for OECD and non-OECD countries](   https://data.oecd.org/healthres/nurses.htm) available on GitHub as   [`OECD_nurses`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/OECD_nurses.csv).    [Source for Singapore](   https://data.gov.sg/dataset/healthcare-professional-to-population-ratio)   available on GitHub as [`SG_DrsNurses`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/SG_DrsNurses.csv).        |
|     4    |     Per_1000        |     The values   of   `Resource`. They are measured per   1000 inhabitants.    |
|     5    |     pct_GDP        |     The   government’s spending on healthcare as a   percentage of GDP for that   particular   year. [Source for for OECD and non-OECD countries](   https://data.oecd.org/healthres/health-spending.htm) available on GitHub   as [`OECD_healthGDP`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/OECD_healthGDP.csv).   [Source for Singapore](   https://data.gov.sg/dataset/government-health-expenditure?view_id=cdc03adc-b1b0-4eaa-99e2-269b174d1ef4&resource_id=cf7b1696-9b0e-425d-a96a-e61c41629623)   available on GitHub as   [`SG_healthGDP`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/SG_healthGDP.csv).        |
|     6    |     avg_GDP    |     The mean   healthcare spending (as measured as percentage of GDP) from 2008-2017.    |
|     7    |     avg_GDP_rankByincome    |     The ranking   of `avg_GDP` based on `Income_group`. The higher the ranking, the higher the   average healthcare expenditure for that income bracket.     |
|     8    |     pct_Elder      |     Percentage   of   the population above 65 years old.   [Source for OECD and non-OECD countries](   https://data.oecd.org/pop/elderly-population.htm)  available on GitHub as [`OECD_ElderPop`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/OECD_ElderPop.csv).   [Source for Singapore](   https://data.gov.sg/dataset/key-indicators-on-the-elderly-annual?view_id=2c681267-b071-41ca-a96e-3a7d7a144ddb&resource_id=f54142e2-7490-42d3-a104-4d6e9fe79881)  available on GitHub as   [`SG_ElderPop`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/SG_ElderPop.csv).      |
|     9    |     OECD    |     [OECD   membership     status](http://www.oecd.org/about/members-and-partners).   There are 34 OECD countries, 6 Non- OECD countries and Singapore in   this dataset.    |
|     10    |     CountryVsSG_bed    |     Whether   a   country has more or fewer beds in a   particular year compared to Singapore.    |
|     11    |     CountryVsSG_drs    |     Whether   a   country has more or fewer doctors in   a particular year compared to Singapore.      |
|     12    |     CountryVsSG_nurses        |     Whether   a   country has more or fewer nurses in   a particular year compared to Singapore.    |
|     13    |     Income_group      |     The   country’s   income group as determined   by the [World Bank]( http://databank.worldbank.org/data/download/site-content/CLASS.xls),   available on GitHub as [`world bank income   bracket`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/world%20bank%20income%20bracket.xls).       |
### Secondary dataset [`df_top5resource2017`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/df_top5resource2017.csv)
It contains the top 5 nations and Singapore for each `Resource` in `Year` 2017 and the average of the top 5 nations.
|     #    |     Variable    |     Meaning    |
|-|-|-|
|     1    |     Year    |     2017. The last `Year` in the primary   dataset was selected to have the most up to date figures for comparison.           |
|     2    |     Resource    |     The three resources in the primary   dataset, `Bed`, `Dr`, `Nurse`.          |
|     3    |     Country    |     Top 5 countries for each `Resource` and   Singapore          |
|     4    |     per_1000    |     The values of `Resource`. They are   measured per 1000 inhabitants.           |
|     5    |     avgTop5_per1000    |     Average of the top 5 nations. The   average acts as a baseline to compare the extend of the resource shortfall.          |

# Storytelling
Freystag’s Pyramid was adopted as the narrative framework for data storytelling. 
![](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/images/Intro.png)
<br>
<br>
![](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/images/nurse%20shot.png)

## Recommendations
The average of the top 5 nations for each resource is used as a benchmark for the number of resources Singapore should aim for. Based on this benchmark, Singapore needs to double the number of doctors, beds and nurses. 

