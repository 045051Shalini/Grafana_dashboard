# Real Time Weather Monitoring and Analysis 

# Objectives

## Weather Pattern Monitoring:

i) Track real-time weather conditions
ii) Monitor extreme weather events
iii) Analyze daily temperature variations
iv) Study relationship between humidity and pressure

## Resource Management:

i) Optimize energy usage based on temperature patterns
ii) Plan outdoor activities around weather conditions
iii) Manage water resources using rainfall and evaporation data

## Risk Assessment:

i) Monitor extreme wind events
ii) Track rainfall patterns for flood risk
iii)Analyze pressure changes for storm prediction


# Description of Dataset

The dataset includes multiple rows of observations, each corresponding to a specific time or day, with values for each column reflecting weather conditions at that time.
It provides a rich set of normalized and raw weather data suitable for statistical analysis and machine learning applications in meteorology and climate studies.


Dataset Attributes:

## 1.Temperature-related:

i) temp9am, temp3pm: Temperature readings at 9AM and 3PM
ii) min_temp, max_temp: Daily minimum and maximum temperatures
Real-time temperature variation (shown in dashboard)

## 2.Wind-related:

i) wind_dir9am, wind_dir3pm: Wind direction at 9AM and 3PM
ii) wind_gust_dir: Wind gust direction
iii) wind_gust_speed: Speed of wind gusts
iv) windspeed9am, windspeed3pm: Wind speeds at 9AM and 3PM

## 3.Atmospheric conditions:

i) pressure9am, pressure3pm: Atmospheric pressure readings
ii) humidity9am: Morning humidity levels
iii) rainfall: Precipitation amount
iv) evaporation: Water evaporation rate
v) sunshine: Hours of sunshine
vi) rain_today_code: Binary indicator for rainfall

# Queries

## 1. Pie Chart: Rain Today Status
InfluxQL Query:
sql
Copy code
SELECT COUNT("rain_today_code") 
FROM "weather_data" 
WHERE time > now() - 1h 
GROUP BY "rain_today_code"
Purpose: Show the proportion of locations reporting rain in the last hour.


## 2. Heatmap: Humidity and Pressure Relationship
InfluxQL Query:
sql
Copy code
SELECT MEAN("humidity9am"), MEAN("pressure9am") 
FROM "weather_data" 
WHERE time > now() - 1h 
GROUP BY time(1m) fill(null)
Purpose: Correlate humidity and pressure trends in the past hour with minute-level granularity.

## 3. Extreme Wind Gust Events 
Table: Extreme Wind Gust Events (Real-Time Alerts)*
*InfluxQL Query*:
sql
SELECT "time", "location", "wind_gust_speed" 
FROM "weather_data" 
WHERE time > now() - 1h 
AND "wind_gust_speed" > 40

*Purpose*: Display wind gust events exceeding 40 in the last hour.  
*Visualization*: Table with alerts.


## 4.  Real-Time Humidity and Pressure (Grouped Hourly)*
*InfluxQL Query*:
sql
SELECT MEAN("humidity9am"), MEAN("pressure9am") 
FROM "weather_data" 
WHERE time > now() - 1h 
GROUP BY time(5m) fill(null)

*Purpose*: Monitor real-time humidity and pressure, grouped every 5 minutes for the last hour.  
*Visualization*: Multi-line graph.

## 5. Scatter Plot: Sunshine vs. Evaporation*
*InfluxQL Query*:
sql
SELECT "sunshine", "evaporation", "wind_gust_speed" 
FROM "weather_data" 
WHERE time > now() - 1h 
AND "sunshine" > 0 AND "evaporation" > 0

*Purpose*: Explore the relationship between sunshine and evaporation, scaled by wind gust speed, in real time.  
*Visualization*: Scatter plot.

## 6. Gauge: Maximum Temperature in the Last Hour
InfluxQL Query:
sql
Copy code
SELECT MAX("max_temp") 
FROM "weather_data" 
WHERE time > now() - 1h
Purpose: Display the highest recorded temperature in the last hour.

## 7. Stacked Bar Chart: Wind Speeds (9AM vs 3PM) by Location*
*InfluxQL Query*:
sql
SELECT MEAN("windspeed9am"), MEAN("windspeed3pm") 
FROM "weather_data" 
WHERE time > now() - 1h 
GROUP BY "location" fill(null)

*Purpose*: Compare wind speeds at 9 AM and 3 PM across locations for the last hour.  
*Visualization*: Stacked bar chart.

## 8. Time Series: Real-Time Temperature Variation*
*InfluxQL Query*:
sql
SELECT MEAN("max_temp"), MEAN("min_temp") 
FROM "weather_data" 
WHERE time > now() - 1h 
GROUP BY time(5m) fill(null)

*Purpose*: Show real-time temperature variation (max and min) in 5-minute intervals for the last hour.  
*Visualization*: Multi-line graph.

# Managerial Insights 

## Weather Pattern Monitoring:

i) Current Rain Today Status shows 57, indicating moderate rainfall conditions that require attention for weather-dependent operations.

ii) Real-time humidity readings of 0.800 and 0.574 suggest high moisture content in the air, which could impact indoor climate control systems.

iii) Temperature variation graph shows consistent fluctuation between 20-25°C over time periods (01:10 to 01:30), indicating stable thermal conditions
Maximum temperature of 40.4° suggests the need for heat stress management protocols during peak hours.

## Resource Management:

i) Sunshine value of 5.19 hours versus evaporation rate of 67.2 indicates high evaporation despite moderate sunshine, suggesting efficient water management strategies are needed

ii) The dashboard shows significant wind variation (35 units in wind gust data), which could be leveraged for renewable energy planning during peak wind periods

iii) Temperature patterns shown in the real-time variation graph can help optimize HVAC system operations across different time periods

## Risk Assessment:

i) Extreme Wind Gust Events graph shows multiple spikes reaching 50 units between 01:10-01:30, indicating potential safety risks for outdoor operations

ii) The humidity-pressure relationship display (shown in bar format) reveals periodic fluctuations that could signal approaching weather changes

iii) Wind speeds comparison across locations (shown in the colored bands: green, yellow, blue, orange) helps identify high-risk zones requiring different safety protocols





