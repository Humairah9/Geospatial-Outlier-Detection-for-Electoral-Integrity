# Geospatial-Outlier-Detection-for-Electoral-Integrity
Analyzed Kwara State election data using Python and Tableau to detect voting anomalies. Applied clustering (DBSCAN) and anomaly detection (Isolation Forest, Moran’s I, Getis-Ord Gi) to flag outlier polling units and visualize spatial patterns that support electoral transparency.

 # Table of content
   - [Introduction](https://github.com/Humairah9/Geospatial-Outlier-Detection-for-Electoral-Integrity/blob/main/README.md#introduction)
   - [Objectives](https://github.com/Humairah9/Geospatial-Outlier-Detection-for-Electoral-Integrity/blob/main/README.md#objectives)
   - [Scope of the Analysis](https://github.com/Humairah9/Geospatial-Outlier-Detection-for-Electoral-Integrity/blob/main/README.md#scope-of-the-analysis)
   - [Methodology](https://github.com/Humairah9/Geospatial-Outlier-Detection-for-Electoral-Integrity/blob/main/README.md#methodology)
     
   


![istockphoto-1200321063-612x612](https://github.com/user-attachments/assets/cdd0b772-ba10-4b25-b88d-32d95bbd0c04)

# Introduction 
Following widespread allegations of electoral irregularities, the Independent National Electoral Commission (INEC) mandated an in-depth analysis of voting patterns to identify potential anomalies. This report provides a detailed analysis of polling unit data for Kwara State using geospatial and statistical methods to detect outlier voting behaviors.
The study integrates multiple data sources, including electoral results, polling unit locations, and demographic indicators, to assess the integrity of the voting process. Advanced statistical techniques, such as anomaly detection and clustering, are applied to uncover irregular patterns that may indicate potential electoral malpractices. Additionally, the analysis considers socio-economic factors that may influence voter behavior, ensuring a more nuanced understanding of the electoral landscape.
By leveraging geospatial analytics, this report aims to provide evidence-based insights that can inform policy decisions, enhance electoral transparency, and support efforts to strengthen democratic processes. The findings will be instrumental in identifying areas that require further investigation and ensuring the credibility of electoral outcomes.

# Objectives 
The primary objectives of this analysis are:
- To enhance dataset accuracy by integrating geospatial coordinates and socio-economic factors.
- To employ geospatial clustering methods to identify polling units with significant deviations.
- To calculate outlier scores using advanced statistical and machine learning techniques.
- To perform temporal and demographic analysis to detect irregularities.
- To develop an interactive visualization dashboard for stakeholders.
- To provide actionable recommendations for improving election integrity.

# Scope of the Analysis
The scope of this study encompasses the detection of electoral anomalies in Kwara State using statistical and geospatial analysis. The analysis focuses on identifying outlier voting behaviors at the polling unit level based on electoral data, geographic information, and socio-economic factors.

# Methodology
- Data Collection: The dataset used for this analysis, KWARA_crosschecked.csv, was obtained from the Independent National Electoral Commission (INEC) records and publicly available election data sources. It contains detailed polling unit information, including the number of accredited voters, registered voters, results for various political parties, and the status of result sheets. The dataset was cross-checked for accuracy and completeness to ensure the reliability of the analysis.
- 2.2	Data Processing and Cleaning: The script below retrieves latitude and longitude coordinates for addresses in a DataFrame using the Google Maps Geocoding API. It defines a function to fetch coordinates, initializes empty latitude and longitude columns, and loops through each row to construct an address. The API is called for each address, and the resulting coordinates are stored in the DataFrame. A 1-second delay is added between requests to prevent hitting API limits. Finally, the updated DataFrame is saved as "geocoded_dataset.csv".

  Key preprocessing steps included:
  - Cleaning and validating data to ensure consistency and eliminate missing values.
  - Ensuring all polling units had latitude and longitude values for geospatial analysis.
    
![image](https://github.com/user-attachments/assets/a9475f65-94c0-44ba-acf0-cdb71ecc18fa)

- Statistical & Geospatial Techniques: The scatter plot below shows polling unit locations, with most points clustered in Nigeria’s expected range. However, a few points are far outside this range, indicating possible geolocation errors or anomalies in the dataset.
  
![image](https://github.com/user-attachments/assets/c1fb7460-b900-43f0-9f02-989b1a19de15)

- Distribution Analysis to Check Voters Trend: The histogram chart below shows that vote distributions are right-skewed, with most polling units having low vote counts. APC and PDP have broader distributions, while LP and NNPP have a high concentration of low vote counts. This helps in analyzing voting patterns and detecting anomalies.

  ![image](https://github.com/user-attachments/assets/360f16d0-b9c9-4895-8af2-f0eb288a4e4a)

- Anomaly Detection Methods
   - DBSCAN Sensitivity Analysis: Geospatial clustering was performed using DBSCAN to detect outlier polling units based on latitude and longitude. It converts coordinates to radians, standardizes the data, and runs DBSCAN at different neighborhood radii (500m, 1km, 2km).
   - Sensitivity analysis was also conducted at radii of 500m, 1km, and 2km to assess outlier stability across different spatial scales. The output shows that more outliers are detected at smaller radii (771 at 500m, 579 at 1km, 448 at 2km), indicating that polling units are more isolated at shorter distances but form clusters at larger scales.

- Statistical Outlier Detection Methods: Statistical Outlier Detection Methods Outlier scores for each polling unit were computed using:
  - Local Moran’s I: Measured local spatial autocorrelation to detect unusually high or low voter concentrations relative to neighboring polling units. The code performs a spatial autocorrelation analysis using Local Moran’s I for APC votes. It converts location data into a GeoDataFrame, creates a spatial weights matrix (K-Nearest Neighbors), computes Local Moran’s I scores, identifies statistically significant outliers (p < 0.05), and visualizes the distribution of Moran’s I scores in a histogram.

![image](https://github.com/user-attachments/assets/63ed5519-9f16-495a-bfaf-e965877b3330)

The four histograms illustrate the distribution of Local Moran’s I scores for APC, LP, PDP, and NNPP, measuring spatial autocorrelation in voting patterns. Most values cluster around zero, indicating that voting patterns are mostly random or weakly spatially structured. However, the presence of extreme values suggests localized clusters where voting behavior significantly deviates from the surrounding areas. These outliers may indicate strong party dominance in certain regions or unusual voting patterns that warrant further investigation. This spatial analysis helps identify areas with significant clustering, which could be useful for electoral strategy, fraud detection, or understanding voter behavior. 

  - Getis-Ord Gi (Hot Spot Analysis): Identified statistically significant clusters of high or low voter turnout, revealing potential manipulation hotspots. The histograms below show most Z-scores near zero, indicating weak spatial clustering, but some extreme values suggest localized clusters. APC and PDP have more dispersed distributions, while LP and NNPP show skewed patterns with fewer strong clusters. This analysis highlights areas of significant voting concentration.

![image](https://github.com/user-attachments/assets/1e8fad7c-9bc7-4ea5-b5c6-244925e8f67b)

   - Isolation Forest: A machine learning-based anomaly detection method that validated statistical findings by analyzing multi-dimensional electoral patterns. The table below displays polling units with different spatial anomaly detection results. The Moran’s I outlier column identifies ONIYEYE OPEN SPACE and LAODU 1 OPEN SPACE as spatial anomalies, suggesting irregular voting patterns. However, no locations are classified as hotspots or coldspots based on the Getis-Ord Gi* statistic, meaning no strong clustering of high or low votes. Additionally, no polling units are flagged as outliers using the Isolation Forest method. The results indicate that only Moran’s I detected outliers, suggesting localized irregularities rather than broad clustering effects.

![image](https://github.com/user-attachments/assets/2f8e3c3c-e126-433e-90a9-e76be857dc68)

# Findings and Key Anomalies
- The analysis reveals that APC and PDP votes moderately correlate, suggesting overlapping support bases, while LP tends to perform slightly worse in areas with strong PDP support. Employment rate shows little influence on voting patterns, but population and employed population are highly correlated, as expected.
- APC leads in most LGAs with the highest vote counts, followed by PDP as the main rival with varying support. LP and NNPP show minimal influence, while Ilorin West stands out with the highest overall vote count, underscoring its political importance.
- The analysis detects polling units with abnormal voting patterns using spatial and anomaly detection methods. Flags like "Moran Outlier" and "Hotspot" highlight significant deviations, with ONIYEYE OPEN SPACE and LAODU 1 OPEN SPACE standing out as potential indicators of irregularities.
- The vote totals show APC leading with 222,568 votes, followed by PDP with 114,610, while LP and NNPP lag far behind with 28,407 and 2,824 votes respectively, indicating a strong advantage for APC.
- A bar chart highlights polling units with the most registered voters, led by OSERE JUNCTION, GWARIA KLGEA SCH, and IN FRONT OF JAGUN MOSQUE, aiding in pinpointing high-turnout areas.
- A map uses dot sizes to represent registered voters across LGAs in Kwara State, with larger dots indicating areas of higher voter registration.
- A geospatial map displays total votes per LGA using red dots, where larger dots indicate higher vote counts, with a notable concentration around Ilorin, suggesting greater voter engagement there.
- The bubble chart illustrates party dominance by LGA, with bubble size reflecting total votes. Ilorin West and Ilorin South stand out with the largest bubbles, indicating the highest vote counts, while colors differentiate the leading parties in each area.
  
# Visualizations 
![image](https://github.com/user-attachments/assets/e92cea94-876b-4c51-81d2-531a02d7d40c)

![image](https://github.com/user-attachments/assets/eb4fa1e6-f3af-477c-bffb-92ff11529879)

![image](https://github.com/user-attachments/assets/e8a88210-3f97-4eec-90c8-c79118088246)

# Conclusion
This analysis provides an evidence-based approach to detecting electoral irregularities. By leveraging geospatial analytics, statistical methods, machine learning, and socio-economic insights, we have identified key polling units requiring further investigation. These insights aim to enhance electoral integrity and transparency for future elections.

# Recommendations
Based on the detected anomalies, we propose the following:
- Conduct forensic audits of high-risk polling units with unusual turnout trends.
- Investigate result sheet discrepancies, particularly in unsigned or unclear cases, as they correlate with anomalies in employment and literacy data.
- Implement stricter verification processes for voter accreditation, especially in clusters identified as high-risk via geospatial analysis.
- Deploy real-time anomaly detection systems for future elections, incorporating both electoral and socio-economic data.
