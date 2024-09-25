# Load Disaggregation
Unsupervised learning model to disaggregate building HVAC heating and cooling load (time series) from the total building electricity load 

## Data preperation
1. Calculate total building load
    total_load(kW) = main_meter(kW) + PV_battery_system(kW)  
There shouldn't have negative values in total_load(kW).

Nigative values are rounded to 0.

2. Visualize total_load(kW) to understand the patterns of the data
Pay attention to weekly and seasonal patterns for different building types: office, school, nursing home, shopping center, kindergarten.

3. Merge the load csv files with corresponding weather csv files
All weather files are in 1 hour resolution. When combined with building load files at different time resolution, interpolation of weather files can be considered.

## Data cleaning
Drop rows with missing values (alternative: filling missing values with mean/median or other imputation techniques). No need to fill them becasue there are no recordings to validate.

Handling outliers (using e.x. IQR method etc.). But perhaps it is better choose not to handle the "outliers" as these may represent extreme weather conditions, so they are actually not outliers.

Handling improper values. Values in the columns of "total_load(kW)", "direct_solar_radiation(W/m^2)" and "diffuse_solar_radiation(W/m^2)" should not be negative. All negative values in these columns should be rounded to 0.

Data type conversion: Ensure all columns have appropriate data types. "timestamp" in datatime, others in numerical values.

Feature creation and handling cyclical features: Create additional time-based features such as hour, day_of_week etc. and use sine/cosine transformation.

Data normalisation: Normalise or standerdise usually comes at the last step of data cleaning. The values to make sure they are in the same scale.
