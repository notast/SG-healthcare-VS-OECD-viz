# Background 
The current Singapore healthcare landscape is painted in a storyboard against OECD and non-OECD peers to understand if more resources are warranted in view of a greying poupulation, tension between adequate resources versus overspending is also addressed. 

## Software 
Storyboard was done in `Tableau`. Data preparation was done with `R`'s `tidyverse`, `rvest`, `countrycode`. 

# Data
There are two datasets. The primary dataset has 1080 rows and 13 columns. The primary dataset consists of data from various sources. Variables from various sources were matched as close as possible based on available meta-data. The secondary dataset has 36 rows and 9 columns. It consists of aggerated values from the primary dataset. 

## Multiple Sources
Rudimentary, healthcare provision includes the number of beds, doctors and nurses a country has. Nonetheless, it will be myopic to operate healthcare on a unilateral plane, healthcare needs to be treated as a multi-disciplinary field for more optimal provision. Thus, additional data such as demography (e.g. the proportion elderly population `pct_Elder`) and economic status (e.g. healthcare spending expressed as share of GDP `pct_GDP` and income status of the country `Income_group`) were included. To complete the analysis, an outcome measure, life expectancy at 65 years old `years_aft65`, was used for evaluation. 

The multiple sources are from international organizations (e.g. Organisation for Economic Co-operation and Development and World Bank) and national organizations (e.g. Government of Singapore’s data repository, data.gov.sg, and its department of statistics). 

## Data dictionary 
### Primary dataset [`df_all`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/df_all.csv) 
|     #    |     Variable    |     Meaning    |
|-|-|-|
|     1    |     Country    |     36 countries   including Singapore. Country names were standardized to the names used in [`R`’s `countrycode` package](https://vincentarelbundock.github.io/countrycode/)  |
|     2    |     Year     |     2008-2017. An   attempt was made to use the most up to date data but data after 2017 from   some sources were not available. A decade’s worth of data was used to reveal   any trends.    |
|     3    |     Resource    |     There are   three types of `resources` per year and country as dataset is in a long tidy   format. <br> `Bed` refers   to beds for acute care, psychiatric care, rehabilitation, long term care   (e.g. nursing homes) and other care needs (e.g. palliative). [Source for OECD   and non-OECD countries]( https://data.oecd.org/healtheqt/hospital-beds.htm) available on GitHub as [`OECD_beds`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/OECD_beds.csv).[Source   for Singapore]( https://www.tablebuilder.singstat.gov.sg/publicfacing/createDataTable.action?refId=15276) available on GitHub as [`SG_bed(abs num)`]( https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/SG_bed(abs%20num).csv). <br> `Dr` refers to   doctors. [Source for OECD and non-OECD countries]( https://data.oecd.org/healthres/doctors.htm) available on GitHub as [`OECD_Drs`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/OECD_Drs.csv).    [Source for Singapore]( https://data.gov.sg/dataset/healthcare-professional-to-population-ratio) available on GitHub as [`SG_DrsNurses`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/SG_DrsNurses.csv). <br> `Nurse` refers   to nurses.[Source for OECD and non-OECD countries]( https://data.oecd.org/healthres/nurses.htm) available on GitHub as [`OECD_nurses`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/OECD_nurses.csv).    [Source for Singapore]( https://data.gov.sg/dataset/healthcare-professional-to-population-ratio) available on GitHub as [`SG_DrsNurses`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/SG_DrsNurses.csv).     |
|     4    |     Per_1000    |     The values of   `Resource`. They are measured per 1000 inhabitants.     |
|     5    |     pct_GDP    |     The   government’s spending on healthcare as a percentage of GDP for that   particular year. [Source for for OECD and non-OECD countries]( https://data.oecd.org/healthres/health-spending.htm) available on GitHub   as [`OECD_healthGDP`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/OECD_healthGDP.csv).   [Source for Singapore]( https://data.gov.sg/dataset/government-health-expenditure?view_id=cdc03adc-b1b0-4eaa-99e2-269b174d1ef4&resource_id=cf7b1696-9b0e-425d-a96a-e61c41629623) available on GitHub as [`SG_healthGDP`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/SG_healthGDP.csv).    |
|     6    |     pct_Elder    |     Percentage of   the population above 65 years old. [Source for OECD and non-OECD countries]( https://data.oecd.org/pop/elderly-population.htm)  available on GitHub as [`OECD_ElderPop`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/OECD_ElderPop.csv).   [Source for Singapore]( https://data.gov.sg/dataset/key-indicators-on-the-elderly-annual?view_id=2c681267-b071-41ca-a96e-3a7d7a144ddb&resource_id=f54142e2-7490-42d3-a104-4d6e9fe79881)  available on GitHub as [`SG_ElderPop`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/SG_ElderPop.csv).    |
|     7    |     years_aft65    |     Life   expectancy at 65 years old; in other words, the average number of years a   person at 65 years old can be expected to live. [Source for OECD and non-OECD   countries]( https://data.oecd.org/healthstat/life-expectancy-at-65.htm)   available on GitHub as [`OECD_LifeExp65`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/OECD_LifeExp65.csv).   [Source for Singapore]( https://data.gov.sg/dataset/key-indicators-on-the-elderly-annual?view_id=3c7f4859-a243-4c17-82fb-7c3f1bc6f403&resource_id=a090d6d7-0e60-4882-9c23-933cc5854902)   available on GitHub as [`SG_LifeExp65`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/SG_LifeExp65.csv).     |
|     8    |     OECD    |     [OECD membership   status](http://www.oecd.org/about/members-and-partners).   There are 32 OECD countries, 3 Non- OECD countries and Singapore in this   dataset.    |
|     9    |     CountryVsSG_beds    |     Whether a   country has more or fewer beds in a particular year compared to Singapore.     |
|     10    |     CountryVsSG_drs    |     Whether a   country has more or fewer doctors in a particular year compared to Singapore.       |
|     11    |     CountryVsSG_nurses    |     Whether a   country has more or fewer nurses in a particular year compared to Singapore.     |
|     12    |     CountryVsSG_GDP    |     Whether a   country spends more or less on healthcare against its GDP in a particular   year compared to Singapore.     |
|     13    |     Income_group    |     The country’s   income group as determined by the [World Bank]( http://databank.worldbank.org/data/download/site-content/CLASS.xls),   available on GitHub as [`world bank income bracket`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/world%20bank%20income%20bracket.xls).    |

### Secondary dataset [`df_outcomeVSgdp`](https://github.com/notast/SG-healthcare-VS-OECD-viz/blob/main/df_outcomeVSgdp.csv)
|     #    |     Variable    |     Meaning    |
|-|-|-|
|     1    |     Country    |     All 36   countries from the primary dataset          |
|     2    |     change_GDP    |     The absolute   change in healthcare spending (as measured as percentage of GDP) in 2017   compared to 2008. <br> _E.g. Spending   in 2017 is 10% of GDP and spending in 2008 is 3% of GDP, `change_GDP` will be   7%._           |
|     3    |     change_GDP_R    |     The ranking of   `change_GDP`. The higher the ranking, the more the country spent on   healthcare in 2017 compared to 2008.           |
|     4    |     Change_years    |     The absolute   change in the number of years for life expectancy at 65 years old in 2017   compared to 2008.           |
|     5    |     avg_GDP    |     The mean   healthcare spending (as measured as percentage of GDP) from 2008-2007.          |
|     6    |     avg_GDP_R    |     The ranking of   `avg_GDP`. The higher the ranking, the higher the average healthcare   expenditure.           |
|     7    |     avgY2YDiff_GDP    |     The mean year   to year difference of healthcare expenses (as measured as percentage of GDP). <br> _E.g. Spending   in 2007 is 4% of GDP, spending in 2008 is 6% of GDP, spending in 2009 is 7%.   Year to year difference for 2007-2008, will be 2% and year to year difference   for 2008-2009 will be 1%. The average year to year difference will be 1.5%._          |
|     8    |     avgY2YDiff_years    |     The mean year   to year difference of years for life expectancy at 65 years old.          |
|     9    |     avgY2YDiff_elder    |     The mean year   to year difference of elderly population.           |

# EDA
TBA
