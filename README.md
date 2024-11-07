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

- **Output**:

  ![Accident_severity](https://github.com/OchePrince/Road-Accident-Data-Analysis/blob/main/images/Accident_severity%20count.png)

  ![light_conditions](https://github.com/OchePrince/Road-Accident-Data-Analysis/blob/main/images/light_conditions.png)

- **Key Findings**:
    1. **Severity Distribution**: Slight accidents make up the majority of cases, followed by serious and fatal accidents.
    2. **Light Conditions**: The data shows that majority of accident occur during the day than night, this could be, because during the day the road is always busya and less busy at night.

### Bivariate Analysis
**Goal**: To examine relationships between pairs of variables.
- **Accident Severity by Road Type**:  Analyzed how different road types are associated with accident severity levels.
- **SQL CODE**:
     ```SQL
                  -- Total accident and casualties by Road Type
        SELECT 
            Road_Type,
            Accident_Severity,
            COUNT(*) AS Total_Accdent
        FROM road_accident_data
        GROUP BY Road_Type, Accident_Severity
        ORDER BY 2 DESC;

- **OutPut**:

   ![Roadtype accident](https://github.com/OchePrince/Road-Accident-Data-Analysis/blob/main/images/Roadtype.png)

- **Key Findings**
1. **Single Carriageway Dominance**:
   - *Slight Accidents*: The majority of slight accidents occur on single carriageways (195,185), indicating high accident frequency but generally low severity.
   - *Serious and Fatal Accidents*: Single carriageways also have the highest counts for serious (32,444) and fatal accidents (2,982), suggesting they are high-risk areas for both high-frequency and high-severity accidents.
2. **Dual Carriageway Accidents**: Dual carriageways have a significant number of slight (39,314) and serious (5,331) accidents. However, they have fewer fatalities (822) compared to single carriageways. Dual carriageways might benefit from safety measures aimed at reducing serious accidents, potentially focusing on speed regulation or barrier enhancements.
3. **Roundabouts and One-Way Streets**:    
   - *Slight Accidents*: Roundabouts and one-way streets primarily see slight accidents (19,070 and 5,402, respectively), possibly due to lower speeds but complex maneuvering.
   - *Serious and Fatal Accidents*: Roundabouts report fewer serious (1,782) and fatal (77) incidents, and one-way streets show similarly low fatality counts.
   - Roundabouts and one-way streets are relatively safer, but adjustments such as clearer signage or optimized traffic flow might reduce the likelihood of serious accidents.
4. Slip Roads: Slip roads show minimal accidents overall, but fatalities do occur occasionally (14 fatalities). This might indicate the need for better marking, lighting, or merging control in these areas.

5. **Missing data(NA)**: Records marked "NA" for road type appear across all severity levels but in small numbers. Investigating this missing data could clarify if these cases share any common characteristics.

- **Recommendations**:
   - Single Carriageways: Improve visibility, enforce speed limits, and consider additional road safety features, such as warning signs or rumble strips, particularly in high-traffic zones.
   - Dual Carriageways: Review serious accident sites for potential infrastructure improvements, such as barriers or increased law enforcement presence.
   - Roundabouts: Regular maintenance and visibility improvements could reduce the already low but existent rate of serious and fatal accidents.

### Environmental Conditions on Road Accident
- **Accidents by Weather and Light Conditions**:
   - **Goal**: To find out which weather condition has the most accident record and give recommendations to reduce the amount of accident rate.
   - **SQL CODE**:
      ```SQL
              -- Accidents by Weather and Light Conditions
        SELECT Weather_Conditions, Light_Conditions, COUNT(*) AS Total_Accident
        FROM road_accident_data
        GROUP BY Weather_Conditions, Light_Conditions
        ORDER BY  Weather_Conditions, Light_Conditions;
 
   - **Output**:

      ![weather_condition](https://github.com/OchePrince/Road-Accident-Data-Analysis/blob/main/images/weather_condition.png)

  - **Key Findings**:
     1. **Dominance of 'Fine, No High Winds' Conditions**: Most accidents occur under calm, fair weather conditions, particularly when there are no high winds. During the day, this condition accounts for 188,557 recorded accidents, and it remains high at night with 55,938 incidents. This trend suggests that when the weather is mild, road usage increases, possibly leading to a higher accident rate due to more vehicles on the road.
     2. **Rainy Weather Conditions**: The data shows that when its raining with no high wind there is 21,603 incident during the day and 13,274 accidents at night. Same thing for snowing with no high wind, this generally implies that at low wind or no wind there is a high chance of accident occuring due to increase road usage.
     3. **Fog or Mist Weather Conditions**: Accidents during fog or mist are relatively low compared to other weather conditions, with 763 accidents recorded during the day and a slight increase to 927 at night. This trend suggests that foggy weather likely results in drier roads with reduced traffic, potentially due to drivers being more cautious or avoiding travel under low-visibility conditions.

   - **Recommendations**:
     1. Implement increased traffic monitoring and enforcement during fair weather conditions, especially during high-traffic hours in the day and night. This could include deploying more traffic officers, setting up mobile speed cameras, or introducing electronic speed signage in busy zones.
     2. Install enhanced fog-warning systems and reflective road markers in areas prone to fog or mist. In addition, lower speed limits and increased signage can remind drivers to exercise caution in these conditions.
     3. Run public awareness campaigns focused on the increased risks associated with nighttime driving, particularly in calm weather. Campaigns can promote defensive driving practices and emphasize caution in familiar weather conditions.
     4. Increase the frequency of road treatments like salting, sanding, and plowing in areas prone to snow. Additional attention to high-traffic and high-accident roads can reduce risks associated with ice and snow accumulation.
     5. Snow and ice create slippery surfaces, which greatly increase stopping distances and the risk of skidding. Regular treatments can make roads safer and improve vehicle traction.
     6.  Improve drainage systems on roads susceptible to water accumulation to prevent puddling and hydroplaning hazards. Regular maintenance to keep drains clear of debris is essential, especially in areas with frequent rain. Rain can cause standing water on roadways, which increases the chance of hydroplaning and loss of control. Effective drainage helps maintain dry lanes and reduces these risks.

### Total Accident and Casualties in a Year
- **Goal**: To understand patterns and trends of road accident accross diffrent months and day of the week and also the time when most accident occur and the number of casualties.
- **Number of Accident in a Year and Month and Total Casualties**
   - **SQL CODE**:
      ```SQL
        SELECT 
            `Year`,
            Months,
            COUNT(*) AS Total_Accident,
            SUM(Number_of_Casualties) AS Total_casualties
        FROM road_accident_data
        GROUP BY `Year`, Months
        ORDER BY `Year`, Total_Accident DESC;
 
    - **Output**:

       ![yearly casualties](https://github.com/OchePrince/Road-Accident-Data-Analysis/blob/main/images/yearly%20casualties.png)

    - **Key Findings**:
       - **Peak Accident Period**:
           - In 2021, accident numbers peaked in November with 15,473 accidents and 20,975 casualties. The lowest recorded month was February with 10,950 accidents and total casualties of 14,648.
           - In 2022, November peaked with most accident occurrence with 13,622 accident and 18,439 casulties, while December showed the lowest 9,625 accidents and 13200 casualties.

            This trend suggests a seasonal pattern where accident counts tend to rise towards the end of the year (November) and are generally lower at the beginning (January-February and December).
        - **Yearly Comparison**:
           - Comparing month-by-month figures between 2021 and 2022, there is an overall decline in the number of accidents in 2022. November decreased from 15,473 accidents in 2021 to 13,622 in 2022.
           - This decrease could imply improved road safety measures, changes in traffic patterns, or variations in road conditions or weather.
        - **Notable Mid-Year Trends**:
           - Mid-year months like June, July, and August tend to have relatively high accident counts in both years, suggesting that these months might have specific risk factors—such as increased road travel during summer months.
           - These months are notable for consistently high accident counts, with similar values year-over-year.
    - **Recommendations**:
        - Implement public awareness campaigns and increase traffic enforcement during high-accident months, particularly November and mid-year months (June to August). Since these months show consistently higher accident rates, focused safety campaigns could promote safer driving habits and reduce accident numbers during peak periods.
        - Increase winter-specific road safety measures and vehicle maintenance advisories during the winter months (January-February and November-December). Although accident counts are generally lower in winter months, conditions such as rain, snow, or fog can still contribute to accidents. By preparing drivers with safe winter-driving practices, the risk of accidents in adverse conditions can be reduced.
        - Analyze factors that may have contributed to the overall decline in accidents from 2021 to 2022. Possible areas for investigation include changes in traffic volume, implementation of new safety protocols, or modifications in road infrastructure. Understanding the reasons behind the reduction could help replicate successful measures across other areas or seasons, leading to a sustained decrease in accidents.
        - Increase safety interventions like speed enforcement and roadside assistance in summer (June-August), where accidents remain relatively high.

- **Analysis of Accident Frequency and Severity by Day of the Week**
   - **SQL CODE**:
      ```SQL
        -- Accident by Day of the Week
        SELECT 
        	Day_of_week,
            COUNT(*) AS Total_Accident,
            SUM(Number_of_Casualties) AS Total_casualties
        FROM road_accident_data
        GROUP BY Day_of_week
        ORDER BY Total_casualties DESC;
        
        SELECT 
        	Day_of_week,
            Accident_Severity,
            COUNT(*) AS Total_Accident,
            SUM(Number_of_Casualties) AS Total_casualties
        FROM road_accident_data
        GROUP BY Day_of_week, Accident_Severity
        ORDER BY Day_of_week, Accident_Severity ;

    - **Output**:

       ![day_of_the_week accident](https://github.com/OchePrince/Road-Accident-Data-Analysis/blob/main/images/day_of_the_week%20accident.png)

       ![day of the week](https://github.com/OchePrince/Road-Accident-Data-Analysis/blob/main/images/day%20of%20the%20week.png)

      - **Key Findings**:
         - Friday has the highest accident count with 50,529 incident and total casualties of 68,294, followed by Wednesday. Accident rates appear to increase toward the end of the workweek, particularly from midweek onward
         - The data shows that Friday has the highest count of Slight accidents and Serious accidents, while Sunday has the highest Fatal accident. This may suggest that some drivers adopt riskier behaviors, such as speeding or driving under the influence, on weekends.

         These insights could guide targeted interventions, such as heightened traffic enforcement on Fridays and weekends to mitigate the risk of severe accidents.

      - **Recoommendations**:
         - Given the high number of accidents on Fridays and the elevated fatal accidents on Sundays, targeted enforcement, such as DUI checkpoints, speed monitoring, and traffic patrols, could be implemented on these days. This may help to reduce risky driving behaviors.
         - Launch campaigns focused on safe driving practices, particularly highlighting the dangers of reckless and impaired driving on weekends. Encouraging safe driving through social media, billboards, and radio announcements could increase awareness, especially on Sundays.
         - Collaborate with driving schools or local authorities to offer refresher driving courses or workshops, focusing on defensive driving techniques for high-risk periods (Fridays and Sundays). This can help instill safer driving habits among frequent drivers.
         - Areas like 'Not at junction or within 20 metres' and 'T or staggered junction' have the most frequent Sunday and Friday incident. Installing additional traffic signals, warning systems, and surveillance cameras in these locations may help in reducing accidents and quickly responding to incidents.

        These recommendations aim to improve road safety through a combination of enforcement, awareness, education, and targeted interventions on high-risk days.

### Analysis of Accident Frequency and Severity by Junction Control Type
#### Overview:
This analysis examines the relationship between junction control types and the frequency and severity of accidents. By understanding how different types of traffic control at junctions—such as traffic signals, stop signs, and uncontrolled junctions—correlate with accident rates, we can gain insights into the safety impact of various control measures. This assessment can help identify areas where additional control measures or interventions might reduce accident rates and severity.

- **Goal**: The goal of this analysis is to identify high-risk junction types and guide infrastructure improvements. Enhanced safety measures, such as additional traffic signals or warning signs at uncontrolled junctions, could potentially reduce accidents and save lives. The findings will provide actionable insights for urban planners and traffic authorities, aiming to make junctions safer for all road users.

- **Accident Frequency per Junction Control Type**:
   - **SQL CODE**:
      ```SQL
        -- Accident Frequency per Junction Control Type
        SELECT Junction_Control, COUNT(*) AS Total_accident
        FROM road_accident_data
        GROUP BY Junction_Control
        ORDER BY 2 DESC;

    - **Output**:

       ![Junction contro](https://github.com/OchePrince/Road-Accident-Data-Analysis/blob/main/images/Junction%20control.png)

    - **Key Findings**:
       - 150,045 accidents occurred at "Give Way or Uncontrolled" junctions, making it the highest among all junction control types. This suggests that junctions without active control measures may present higher risks, possibly due to increased driver discretion and variability in yielding behavior.
       - 98,055 incidents are marked as "Data Missing or Out of Range," representing a considerable portion of the dataset. This gap in data may limit the ability to draw fully comprehensive conclusions about the effectiveness of specific junction controls and highlights the need for improved data collection methods.
       - "Auto Traffic Signal" junctions have 32,349 accidents, considerably lower than the "Give Way or Uncontrolled" type. This difference indicates that signal-controlled intersections may contribute to safer traffic flow and reduce the likelihood of accidents by enforcing clear yielding patterns.
       - Junctions controlled by "Stop Signs" and "Authorized Personnel" had relatively low accident counts at 1,685 and 460 respectively. These findings suggest that more direct forms of control, such as stop signs or human-directed traffic, might contribute to a decrease in accidents at junctions.
       - There were 25,378 accidents recorded "Not at Junction or Within 20 Metres," which indicates a need to also address road sections that aren't near junctions but might still have accident risks, such as sharp bends or areas prone to congestion.

    - **Recomendations**:
       - Consider adding traffic lights or stop signs at high-traffic uncontrolled junctions. This could help reduce accident rates by minimizing driver ambiguity and encouraging more structured yielding behaviors.
       - To reduce the "Data Missing or Out of Range" cases, traffic authorities should consider revisiting data entry methods and implementing more standardized collection protocols. Accurate data is crucial for informed decision-making and effective safety interventions.
       - Develop public awareness campaigns around safe yielding practices, especially at uncontrolled or "Give Way" junctions. This could include educational materials, road signage reminders, or digital campaigns to encourage cautious driving in these areas.
       - Given the lower accident rates observed at "Auto Traffic Signal" junctions, implementing similar signal controls at other busy junctions could be beneficial. Authorities could analyze high-risk areas to determine where traffic signals would be most effective.
       - While "Stop Sign" junctions have low accident rates, ongoing assessments can ensure they remain effective. Adjusting signage visibility or road markings at these locations could enhance safety further.
       - For the areas recorded "Not at Junction or Within 20 Metres," consider adding cautionary signs, road markings, or speed-reducing measures to address potential risks in non-junction accident-prone zones.

- **Severity Distribution (Slight, Serious, Fatal) Across Junction Control**:
   - **SQL CODE**:
      ```SQL
        SELECT Junction_Control, Accident_Severity, COUNT(*) AS Total_accident
        FROM road_accident_data
        GROUP BY Junction_Control, Accident_Severity
        ORDER BY Junction_Control, Accident_Severity;

    - **Output**:

       ![JUNCTION SEVERITY](https://github.com/OchePrince/Road-Accident-Data-Analysis/blob/main/images/JUNCTION%20SEVERITY.png)

    - **Key Findings**:
       - This category has a high number of fatal (1,916) and serious (15,012) accidents. The lack of precise junction control data here might indicate that certain junctions or road sections with missing control data have elevated risks. This gap in recorded data could also suggest unaccounted or uncontrolled junctions in the system that need attention.
       - Fatal accidents (1,223) and serious accidents (18,237) are notably high in "Give Way or Uncontrolled" junctions. Slight accidents are even more frequent (130,585). This indicates that “Give Way” junctions could pose a higher risk, likely due to the lack of clear yielding instructions, leading to driver uncertainty and more severe accidents.
       - Authorized personnel-controlled areas have very low counts of fatal accidents (2) and serious accidents (42). This low rate implies that direct human control, such as police or traffic wardens, contributes to effective management, particularly in high-risk or temporary traffic conditions.
       - With fatal accidents at 302 and serious at 3,284, "Auto Traffic Signal" junctions show a much lower accident severity compared to uncontrolled junctions. This suggests that signalized intersections are more effective at managing traffic flow and reducing accident severity.
       - There are notable accident numbers at locations "Not at Junction or Within 20 Metres," with fatal accidents at 499 and serious accidents at 3,990. This highlights that road sections just outside junctions may have specific hazards, perhaps due to speeding or sudden changes in traffic conditions near intersections.
       - Fatal accidents (11) and serious accidents (175) at "Stop Sign" junctions are among the lowest in severity, indicating the effectiveness of stop signs in managing traffic safety at low-volume junctions.

    - **Recommendations**:
       - Given the high fatality rates in the "Data Missing or Out of Range" category, focus on improving data recording practices and ensuring all junction types are accounted for. This could reveal unmonitored areas that may benefit from safety interventions.
       - Uncontrolled junctions with high fatality and injury counts may benefit from additional control measures, such as upgrading to traffic signals or adding warning signs. These changes can help reduce the accident severity by providing clearer yielding instructions.
       - Stop sign intersections, despite low severity, could still benefit from improved visibility (such as adding rumble strips) to maintain their safety effectiveness, especially at night or during adverse weather conditions.
       - To address accidents that occur "Not at Junction or Within 20 Metres," implement speed-reducing measures like speed bumps or cautionary signage near these areas. This can help manage the transition into and out of junction areas safely.
       - Auto traffic signals show a reduced severity in accidents. Expanding their use at selected high-risk uncontrolled junctions may be effective in improving overall road safety.
       - Run campaigns to educate drivers on the importance of yielding at “Give Way” junctions and obeying traffic signals. Improved driver awareness can help reduce accident frequency and severity at uncontrolled junctions.
     


### Analysis of Accident Frequency and Severity by Urban and Rural Area
- **Goal**: To know which area has more record of accident incidents and find data-driven solution
- **SQL CODE**:
   ```SQL
    SELECT Urban_or_Rural_Area, COUNT(*) AS Total_accident, SUM(Number_of_Casualties) AS Total_casualties
    FROM road_accident_data
    GROUP BY Urban_or_Rural_Area
    ORDER BY 2 DESC;

- **Output**:

   ![Urban and rural](https://github.com/OchePrince/Road-Accident-Data-Analysis/blob/main/images/Urban%20and%20rural.png)

- **Key Findings**:
  - The Urban area has the highest count of accident with 198532 incident and 255864 casualties.
  - Rural area have a count of 109440 incidents and 162018 casualties.

- **Insights and Recommendations for Accident Frequency by Road Type and Area (Urban vs. Rural)**
- **SQL CODE**:
   ```SQL
    SELECT 
    	Road_Type,
        Urban_or_Rural_Area,
        COUNT(*) AS Total_accident
    FROM road_accident_data
    GROUP BY Road_Type, Urban_or_Rural_Area
    ORDER BY Road_Type, Urban_or_Rural_Area;

- **Output**:

  ![Urban roadtype](https://github.com/OchePrince/Road-Accident-Data-Analysis/blob/main/images/Urban%20roadtype.png)

- **Key Findings**:
   - Single carriageways account for the highest number of accidents in both rural (76,672) and urban (153,939) areas. Urban single carriageways see almost double the accident frequency of their rural counterparts, which may be attributed to higher traffic volume, pedestrian activity, and intersections in urban settings.
   - Dual carriageways have a more balanced accident count between rural (22,333) and urban (23,134) areas. This could indicate that dual carriageways maintain consistent risk levels across both types of environments, possibly due to their design, which often includes central barriers to separate traffic.
   - Roundabouts in urban areas have almost twice the number of accidents (13,504) compared to rural areas (7,425). This may be due to greater congestion and complex traffic flow patterns in urban roundabouts, making them more prone to collisions, especially during peak hours.
   - One-way streets show significantly more accidents in urban areas, with one-way streets at 5,698 (urban) versus 499 (rural). This type of roads, typically more common in urban infrastructure, may see more accidents due to higher traffic density and more frequent lane merging or directional changes.
   - Slip roads show a higher count of accident in the Rural area than in the urban area with 2014 incidents, while 1220 incidents in urban area. This indicate that the slip roads in the rural area are very bad than the urban area.
   - "NA" entries in both rural (497) and urban (1,037) areas are low, indicating that unspecified road types are not as prevalent in the data or have minimal accident occurrences.

- **Recommendations**:
   - Given the high accident rates on single carriageways, especially in urban areas, consider implementing additional traffic-calming measures such as speed bumps, clear lane markings, and improved pedestrian crossings. These measures can help mitigate risks associated with high-traffic single carriageway roads. In rural areas, accidents on single carriageways may stem from high speeds and limited visibility. Adding clear signage, reflective road markers, and additional lighting, particularly at curves or junctions, would improve safety. Routine maintenance to address issues like potholes and lane encroachment is essential.
   - Urban roundabouts experience high accident rates, possibly due to congestion and complex traffic flows. Consider installing clearer signage, advanced traffic lights during peak hours, and speed reduction measures to manage traffic more effectively. In rural roundabouts, enhancing visibility with additional lighting and clear directional signage can reduce the chances of accidents. Public awareness campaigns on navigating roundabouts safely, especially in low-light or foggy conditions, would be beneficial.
   - For dual carriageways, which exhibit similar accident patterns across both environments, maintaining high-quality lane markings, median barriers, and regular road inspections are crucial. Speed monitoring measures, especially in rural areas where drivers might be inclined to speed, can help in maintaining safe driving conditions.
   - Slip roads, more common in urban settings, would benefit from clearly marked merge zones, extended slip lanes, and yield signs. Enhancing lighting and adding speed limits on entry points can help reduce accidents from sudden lane merging. For rural slip roads, where visibility may be limited, reflective markers and warning signs could alert drivers in advance.


### Analysis on the Relationship between Vehicle Types and Road Characteristics on Accident Frequency
#### Overview
This analysis will explore how various vehicle types, speed limit, road characteristics, and carriageway hazards contribute to accident frequency and severity. By examining the intersection of these factors, the goal is to pinpoint specific combinations of vehicle types and road conditions that show a higher propensity for accidents.

- **Summary of Casulties by Vehicle Types**:

  This analysis was done on Excel and the vehicle types where aggregated into; Agricultural vehicle, Cars, Bus, Van, Bike and Others. This was done by using formula to calculate the items and add same fields together

  



   



  



    
          





    
  









       
