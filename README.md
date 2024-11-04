# Road Accident Analysis

## Indroduction
The Road Accident Data Analysis project aims to explore and analyze a comprehensive dataset of road accidents to gain insights into patterns, trends, and contributing factors to road safety. Road accidents are a significant public safety concern worldwide, leading to numerous injuries and fatalities each year. Understanding the underlying causes and trends in these incidents can inform policy decisions, improve road safety measures, and ultimately save lives.

This analysis utilizes a dataset containing detailed information on road accidents, including variables such as accident severity, light conditions, vehicle types, and carriageway hazards. By examining this data, we seek to identify key factors that contribute to road accidents, assess the frequency and severity of accidents under different conditions, and highlight areas where targeted interventions could enhance safety.

The findings from this project will not only contribute to a better understanding of road safety issues but also serve as a valuable resource for stakeholders, including policymakers, road safety organizations, and researchers, who are dedicated to reducing the incidence of road accidents and improving overall traffic safety

---

## Data Overview
- **Data Source**: This Data was gotten from *Kaggle*
- **Descripton**: This data set contains **307,973** rows and 24 columns which include;
    1. Accident_index
    2. Accident_Date
    3. Day_of_week 
    4. Months
    5. Year
    6. Accident_Severity
    7. Light_Conditions
    8. Local_Conditions
    9. Local_Authority_(District)
    10. Carriageway_Hazards
    11. Number_of_Casualties
    12. Police_Force
    13. Road_Surface_Conditions
    14. Road_Type
    15. Speed_limit
    16. Time
    17. Urban_or_Rural_Area
    18. Weather_Conditions
    19. Vehicle_Type
---

## Objectives
The primary objectives of the Road Accident Data Analysis project are as follows:
  - **Identify Trends in Road Accidents**: Analyze the dataset to uncover patterns and trends in road accidents over time, including seasonal variations and yearly changes. This will help in understanding how accident frequency varies across different months and days of the week.
  - **Assess the Impact of Environmental Factors**: Investigate how various environmental conditions, such as Light Conditions *(day vs. night)*, Weather Conditions, and Road Surface Conditions, influence the occurrence and severity of road accidents. Understanding these factors can guide safety improvements.
  - **Examine the Relationship Between Vehicle and Road Characteristics**: Analyze the impact of Vehicle Types, Carriageway Hazards, and Road Types on Accident Severity and frequency. This objective aims to identify which combinations of vehicles and road conditions are most prone to accidents.
  - **Categorize Accidents by Severity**: Classify accidents into different severity levels *(e.g., Fatal, Serious, Slight)* and analyze the data to determine the primary causes of severe accidents. This will assist in prioritizing interventions for high-risk scenarios.
  - **Provide Data-Driven Recommendations**: Based on the analysis results, develop actionable recommendations for stakeholders, including policymakers and road safety organizations, aimed at reducing the number of accidents and enhancing overall road safety.
  - **Facilitate Future Research**: Establish a foundation for further research by documenting the analysis process and findings. This will provide a valuable resource for researchers and practitioners interested in studying road safety issues.

---

## Methodology
- **Data Cleaning**:
    - Microsoft Excel and MySQL was used to clean the data, where duplicates were removed using Excel and filling blank cells with **'NA'**.
    - MySQL was used to combine some column field which are similar and have same meaning for Light Conditions and Road Surface Conditions. Below is the SQL code used to make changes to the data;
  ```SQL
      -- Data Cleaning
    SELECT DISTINCT Road_Surface_Conditions
    FROM road_accident_data;
    
    UPDATE road_accident_data
    SET Road_Surface_Conditions = 'Snow/ice'
    WHERE Road_Surface_Conditions IN ('Frost or ice', 'Snow');
    
    UPDATE road_accident_data
    SET Road_Surface_Conditions = 'Wet'
    WHERE Road_Surface_Conditions IN ('Flood over 3cm. deep', 'Wet or damp');
    
    SELECT DISTINCT Light_Conditions
    FROM road_accident_data;
    
    UPDATE road_accident_data
    SET Light_Conditions = 'Night'
    WHERE Light_Conditions IN ('Darkness - lights lit', 'Darkness - lighting', 'Darkness - lights unlit', 'Darkness - no lighting');

- **Exploratory Analysis**: MySQL and Excel was used to perform analysis on the data to find insights and give Data-driven solutions.

- **Visualization**: Excel was used to create an Interesting and Interactive Dashboard.
---

## Exploratory Data Analysis
The EDA phase focused on examining the Road Accident dataset to identify patterns, relationships, and anomalies. Each step aimed to answer specific questions outlined in the project objectives. The EDA include a combination of summary statistics, data visualizations, and SQL queries to reveal insights into accident trends and contributing factors.
### Data Overview
- **Goal**: To understand the basic structure of the data and check for any immediate issues.
- **Analytical Approach**:
    - Calculated the total number of accidents and reviewed the count of unique entries in key columns Accident_index.
    - Generated summary statistics for numerical columns like Number_of_Casualties, Number_of_Vehicles, and Speed_limit.
- **SQL CODE**:
   ```SQL
       -- Count total records and check unique accident indices
    SELECT COUNT(*) AS Total_Records, COUNT(DISTINCT Accident_index) AS Unique_Accidents
    FROM road_accident_data;
    
    -- Summary statistics for key numerical columns
    SELECT AVG(Number_of_Casualties) AS Avg_Casualties, 
           AVG(Number_of_Vehicles) AS Avg_Vehicles,
           AVG(Speed_limit) AS Avg_Speed_Limit
    FROM road_accident_data;

- **Output**:

  ![unique index](https://github.com/OchePrince/Road-Accident-Data-Analysis/blob/main/images/unique%20index.png)

  ![descriptive_sta](https://github.com/OchePrince/Road-Accident-Data-Analysis/blob/main/images/descriptive_sta.png)

### Univariate Analysis
- **Goal**: To examine individual variables to understand their distribution and frequency.
- **Analytical Approach**:
    - **Accident_Severity**: Understanding the proportion of accidents and total casualties classified as Fatal, Serious, or Slight.
    - **Light_Conditions**: Identifying the total accident and casualties under Day vs. Night conditions.
- **SQL CODE**:
   ```SQL
        -- Accident Severity Insight
    SELECT 
    	Accident_Severity, 
        COUNT(*) AS Total_Accident,
        SUM(Number_of_Casualties) AS Total_casualties
    FROM road_accident_data
    GROUP BY Accident_Severity
    ORDER BY Total_Accident DESC;
    
    -- Accident distribution and Casualties by light conditions
    SELECT Light_Conditions, COUNT(*) AS Accident_Count, SUM(Number_of_Casualties) AS Total_casualties
    FROM road_accident_data
    GROUP BY Light_Conditions; 




    
  









       
