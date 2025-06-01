# Real Time Weather Monitoring and Analysis<br/> 
## Dashboard <br/>

[![Watch the Video](https://img.youtube.com/vi/yHxQ6yRFchk/0.jpg)](https://www.youtube.com/watch?v=yHxQ6yRFchk "Watch the Video")<br/>




![Screenshot 2024-11-24 013529](https://github.com/user-attachments/assets/8040002a-a55e-41be-8c7b-819f6713fbf0) <br/>

# Description of Dataset<br/>

The dataset includes 70k observations, each corresponding to a specific time or day, with values for each column reflecting weather conditions at that time.<br/>
It provides a rich set of normalized and raw weather data suitable for statistical analysis and machine learning applications in meteorology and climate studies.<br/>

## Dataset Attributes:<br/>

### 1.Temperature-related:<br/>

- temp9am, temp3pm: Temperature readings at 9AM and 3PM<br/>
- min_temp, max_temp: Daily minimum and maximum temperatures<br/>
- Real-time temperature variation (shown in dashboard)<br/>

### 2.Wind-related:<br/>

- wind_dir9am, wind_dir3pm: Wind direction at 9AM and 3PM<br/>
- wind_gust_dir: Wind gust direction<br/>
- wind_gust_speed: Speed of wind gusts<br/>
- windspeed9am, windspeed3pm: Wind speeds at 9AM and 3PM<br/>

### 3.Atmospheric conditions:<br/>

- pressure9am, pressure3pm: Atmospheric pressure readings<br/>
- humidity9am: Morning humidity levels<br/>
- rainfall: Precipitation amount<br/>
- evaporation: Water evaporation rate<br/>
- sunshine: Hours of sunshine<br/>
- rain_today_code: Binary indicator for rainfall<br/>


# Objectives<br/>

## Weather Pattern Monitoring:<br/>

- Track real-time weather conditions<br/>
- Monitor extreme weather events<br/>
- Analyze daily temperature variations<br/>
- Study relationship between humidity and pressure<br/>

## Resource Management:<br/>

- Optimize energy usage based on temperature patterns<br/>
- Plan outdoor activities around weather conditions<br/>
- Manage water resources using rainfall and evaporation data<br/>

## Risk Assessment:<br/>

- Monitor extreme wind events<br/>
- Track rainfall patterns for flood risk<br/>
- Analyze pressure changes for storm prediction<br/>


# Queries<br/>

## 1. Guage Chart: Rain Today Status<br/>
InfluxQL Query:<br/>
SELECT COUNT("rain_today_code") <br/>
FROM "weather_data" <br/>
WHERE time > now() - 1h <br/>
GROUP BY "rain_today_code"<br/>
Purpose: Show the proportion of locations reporting rain in the last hour.<br/>

## 2. Heatmap: Humidity and Pressure Relationship<br/>
InfluxQL Query:<br/>
SELECT MEAN("humidity9am"), MEAN("pressure9am") <br/>
FROM "weather_data" <br/>
WHERE time > now() - 1h <br/>
GROUP BY time(1m) fill(null)<br/>
Purpose: Correlate humidity and pressure trends in the past hour with minute-level granularity.<br/>

## 3. Extreme Wind Gust Events <br/>
Table: Extreme Wind Gust Events (Real-Time Alerts)*<br/>
*InfluxQL Query*:<br/>
SELECT "time", "location", "wind_gust_speed" <br/>
FROM "weather_data" <br/>
WHERE time > now() - 1h <br/>
AND "wind_gust_speed" > 40<br/>

*Purpose*: Display wind gust events exceeding 40 in the last hour.  <br/>
*Visualization*: Table with alerts.<br/>


## 4.  Real-Time Humidity and Pressure (Grouped Hourly)*
*InfluxQL Query*:<br/>
SELECT MEAN("humidity9am"), MEAN("pressure9am") <br/>
FROM "weather_data" <br/>
WHERE time > now() - 1h <br/>
GROUP BY time(5m) fill(null)<br/>

*Purpose*: Monitor real-time humidity and pressure, grouped every 5 minutes for the last hour. <br/> 
*Visualization*: Multi-line graph.<br/>

## 5. Scatter Plot: Sunshine vs. Evaporation*<br/>
*InfluxQL Query*:<br/>
SELECT "sunshine", "evaporation", "wind_gust_speed" <br/>
FROM "weather_data" <br/>
WHERE time > now() - 1h <br/>
AND "sunshine" > 0 AND "evaporation" > 0<br/>

*Purpose*: Explore the relationship between sunshine and evaporation, scaled by wind gust speed, in real time.<br/>
*Visualization*: Scatter plot.<br/>

## 6. Gauge: Maximum Temperature in the Last Hour<br/>
InfluxQL Query:<br/>
SELECT MAX("max_temp") <br/>
FROM "weather_data" <br/>
WHERE time > now() - 1h<br/>
Purpose: Display the highest recorded temperature in the last hour.<br/>

## 7. Stacked Bar Chart: Wind Speeds (9AM vs 3PM) by Location*<br/>
*InfluxQL Query*:<br/>
SELECT MEAN("windspeed9am"), MEAN("windspeed3pm") <br/>
FROM "weather_data" <br/>
WHERE time > now() - 1h <br/>
GROUP BY "location" fill(null)<br/>

*Purpose*: Compare wind speeds at 9 AM and 3 PM across locations for the last hour.  <br/>
*Visualization*: Stacked bar chart.<br/>

## 8. Time Series: Real-Time Temperature Variation*
*InfluxQL Query*:<br/>
SELECT MEAN("max_temp"), MEAN("min_temp") <br/>
FROM "weather_data" <br/>
WHERE time > now() - 1h <br/>
GROUP BY time(5m) fill(null)<br/>

*Purpose*: Show real-time temperature variation (max and min) in 5-minute intervals for the last hour. <br/> 
*Visualization*: Multi-line graph.<br/>

# Analysis <br/>

## Weather Pattern Monitoring:<br/>

[![Watch the Video](https://img.youtube.com/vi/uvmCbhy4tFo/0.jpg)](https://www.youtube.com/watch?v=uvmCbhy4tFo "Rain Today Status Video")<br/>

i) Current Rain Today Status shows 71, indicating moderate rainfall conditions that require attention for weather-dependent operations.<br/>

**Managerial Implication:** Moderate rainfall conditions require adjustments in logistics and transportation schedules to avoid delays and ensure safety. Emergency response teams should be on standby in vulnerable regions.<br/>

[![Watch the Video](https://img.youtube.com/vi/ZiYp4JijVwo/0.jpg)](https://www.youtube.com/watch?v=ZiYp4JijVwo "Watch the Video")<br/>

ii) Real-time humidity readings of 0.532 and 0.511 suggest high moisture content in the air, which could impact indoor climate control systems.<br/>

**Managerial Implication:** High humidity levels may increase energy consumption in climate control systems. Managers can optimize HVAC settings or schedule maintenance to handle increased load efficiently.<br/>

[![Watch the Video](https://img.youtube.com/vi/V9WnYtqwNbw/0.jpg)](https://www.youtube.com/watch?v=V9WnYtqwNbw "Watch the Video")<br/>


iii) Temperature variation graph shows consistent fluctuation between 20-25°C over time periods (01:10 to 01:30), indicating stable thermal conditions<br/>

**Managerial Implication:** Stable temperature ranges (20–25°C) reduce the likelihood of extreme heat or cold. This allows for steady outdoor operations and can improve worker productivity.<br/>

[![Watch the Video](https://img.youtube.com/vi/2J3XFfj8elU/0.jpg)](https://www.youtube.com/watch?v=2J3XFfj8elU "Watch the Video")<br/>

Maximum temperature of 39.6° suggests the need for heat stress management protocols during peak hours.<br/>

**Managerial Implication:** Extreme temperatures necessitate heat stress management protocols, such as adjusting work hours, providing cooling facilities, and issuing health advisories to employees working outdoors.<br/>

## Resource Management:<br/>

[![Watch the Video](https://img.youtube.com/vi/RZBKWtW4iig/0.jpg)](https://www.youtube.com/watch?v=RZBKWtW4iig "Watch Rain Today Status Video")<br/>

i) Sunshine value of 8.43 hours versus evaporation rate of 37.4 indicates high evaporation despite moderate sunshine, suggesting efficient water management strategies are needed<br/>

**Managerial Implication:** The high evaporation rate compared to sunshine hours suggests a need for water conservation measures. Irrigation schedules should be optimized to minimize water loss during peak evaporation hours.<br/>

ii) The dashboard shows significant wind variation (57 units in wind gust data), which could be leveraged for renewable energy planning during peak wind periods<br/>
**Managerial Implication:** Large variations in wind gust speeds (up to 57 units) highlight opportunities for wind energy generation. Managers should explore the feasibility of installing wind turbines in high-wind zones.<br/>

iii) Temperature patterns shown in the real-time variation graph can help optimize HVAC system operations across different time periods<br/>

**Managerial Implication:** Real-time temperature data can guide HVAC system adjustments to reduce energy costs. Predictive analytics can improve system efficiency by anticipating thermal conditions.<br/>

## Risk Assessment:<br/>

[![Watch the Video](https://img.youtube.com/vi/LhkfP839mP8/0.jpg)](https://www.youtube.com/watch?v=LhkfP839mP8 "Watch the Video")<br/>

i) Extreme Wind Gust Events graph shows multiple spikes reaching 50 units between 01:10-01:30, indicating potential safety risks for outdoor operations<br/>

**Managerial Implication:** Peaks in wind gust speeds (50+ units) pose safety risks for construction sites, outdoor operations, and transportation. Temporary shutdowns or enhanced safety protocols may be necessary.<br/>

[![Watch the Video](https://img.youtube.com/vi/SC49xJftPho/0.jpg)](https://www.youtube.com/watch?v=SC49xJftPho "Watch the Video")<br/>

ii) The humidity-pressure relationship heat map display reveals periodic fluctuations that could signal approaching weather changes<br/>

**Managerial Implication:** Fluctuations in humidity and pressure could indicate approaching storms or significant weather shifts. This information allows for preemptive measures like securing equipment or issuing early warnings.<br/>

[![Watch the Video](https://img.youtube.com/vi/9CejtUgxYks/0.jpg)](https://www.youtube.com/watch?v=9CejtUgxYks "Watch the Video")<br/>

iii) Wind speeds comparison across locations (shown in the colored bands: green, yellow, blue, orange) helps identify high-risk zones requiring different safety protocols<br/>

**Managerial Implication:** Comparing wind speeds across locations helps identify zones with higher risks. Managers can deploy additional resources, such as reinforced structures or safety gear, in these areas.<br/>




