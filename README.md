# Background 
Like many high-income OECD countries, Singapore is facing with a greying population and it needs to have adequate resources to ride the silver tsunami. However, training and retaining doctors and nurses and building and maintaining hospitals are expensive resulting in tension between having adequate resources versus overspending. 
The storyboard paints the current Singapore healthcare landscape against OECD and non-OECD peers and addresses the dilemma if Singapore needs to scale down its healthcare resources to curb overspending or needs to increase its healthcare resources. 

# Data
There are two datasets. The primary dataset has 1080 rows and 13 columns. The primary dataset consists of data from various sources. Variables from various sources were matched as close as possible based on available meta-data. The secondary dataset has 36 rows and 9 columns. It consists of aggerated values from the primary dataset. 

## Multiple Sources
Rudimentary, healthcare provision includes the number of beds, doctors and nurses a country has. Nonetheless, it will be myopic to operate healthcare on a unilateral plane, healthcare needs to be treated as a multi-disciplinary field for more optimal provision. Thus, additional data such as demography (e.g. the proportion elderly population `pct_Elder`) and economic status (e.g. healthcare spending expressed as share of GDP `pct_GDP` and income status of the country `Income_group`) were included. To complete the analysis, an outcome measure, life expectancy at 65 years old `years_aft65`, was used to evaluate the success of healthcare expenses. 

The multiple sources are from international (e.g. Organisation for Economic Co-operation and Development and World Bank) and national (e.g. Government of Singapore’s data repository, data.gov.sg) organizations. 

## Data dictionary 
