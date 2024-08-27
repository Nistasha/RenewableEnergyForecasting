# Renewable Energy Forecasting

## Problem Statement

- In the face of rising energy prices, the company aims to optimize energy distribution by offering free electricity to customers during surplus periods.
- However, false positives pose a significant risk, potentially resulting in financial losses for the company.

## Objectives

- Develop a predictive model capable of forecasting surplus renewable energy at least 24 hours in advance.
- Minimize false positives to avoid unnecessary costs for the company.
- Provide customers with timely alerts to opt-in for free energy during surplus periods.

## Methodology

### Data Preprocessing

- **Data Cleaning:** Merged all data files into one dataset, identified and filled missing values using Interpolation for numeric data and label encoding for categorical data, resulting in a complete dataset ready for analysis.
- **Feature Engineering:** Extracted relevant features and created additional ones to capture patterns related to energy surplus.

### Model Selection and Training

- Experimented with various time-series forecasting algorithms to identify the most effective one for our purposes.
- Assessed the model's performance through validation techniques, with a particular focus on minimizing false positives.

### Data Visualization

#### Dataset Overview

- Access to historic records spanning from 2010 to December 2023.
- Each record contains hourly observations of various meteorological and environmental parameters, including temperature, humidity, wind speed, solar radiation, etc.

#### Visualization Techniques

- Time series plotting
- Histograms
- Box plots
- Correlation matrix
- Seasonal decomposition

## Feature Engineering

### Wind Energy Generation Calculation

- Assumed a simplified power curve relationship, \( P = V^3 \), where \( P \) is power and \( V \) is wind speed.
- Converted wind speed and direction into vector components to accurately calculate the effective wind speed experienced by the turbine.
- Applied the power curve model to calculate the power output of the turbine for a given wind speed.
- Energy generated is calculated using the formula:  
  \[
  \text{Energy} = P \times t
  \]

### Solar Energy Generation Calculation

- Calculated Solar Panel Efficiency:  
  \[
  \text{Solar Panel Efficiency} = \frac{\text{Energy generated by panels}}{\text{Solar Radiation received}}
  \]
- Estimated Solar Energy Generation:  
  \[
  \text{Solar Energy generated} = \text{Solar radiation} \times \text{Solar Panel Efficiency}
  \]

### Total Renewable Energy Calculation

- Assumed 10 wind turbines and 10 solar panels.
- Calculated total renewable energy:  
  \[
  \text{Total Renewable Energy} = (\text{number of wind turbines} \times \text{wind energy generation}) + (\text{number of solar panels} \times \text{solar energy generation})
  \]

### Total Energy Consumption Estimation

- Estimated the number of households in Brighton (11,895, considering 10% of 118,953 households).
- Used data from British Gas to calculate average hourly consumption per household.
- Introduced variability using a random multiplier \( k \) (ranging from 2 to 10).
- Total energy consumed by households in Brighton:  
  \[
  \text{Total energy consumed} = \text{Estimated number of households} \times \text{Average hourly consumption rate} \times k
  \]

### Calculation of Surplus Energy

- Calculated surplus energy:  
  \[
  \text{Surplus energy} = \text{Total renewable energy} - \text{Energy consumption}
  \]
- Converted surplus values into binary format: 1 indicates surplus, 0 indicates no surplus.
- Aligned surplus status with future data points by shifting the binary values up by 24 rows.

## Modeling

### Data Preparation

- Split dataset into features and the target variable (indicating surplus status of renewable energy).
- Allocated 80% of the dataset for training.

### Model Selection and Training

- Chose four different models: Random Forest Classifier, Decision Tree, K-Nearest Neighbors (KNN), and Logistic Regression.
- Trained each model using the training data and validated using the testing data.

### Evaluation Metrics

- Evaluated model performance, focusing on false positive rates.

## Results

### Model Performance

- **Random Forest Classifier**
  - False Positive Rate: 0.3438
  - Classification Report
  - Confusion Matrix
- **Decision Tree**
  - False Positive Rate: 0.3809
  - Classification Report
  - Confusion Matrix
- **K-Nearest Neighbors**
  - False Positive Rate: 0.4083
  - Classification Report
  - Confusion Matrix
- **Logistic Regression**
  - False Positive Rate: 0.4386
  - Classification Report
  - Confusion Matrix

## Conclusion

- **Random Forest Classifier Outperforms Other Models:** The Random Forest Classifier shows the lowest false positive rate (0.34), making it the most effective model for predicting energy surplus.
- **Model Effectiveness:** The precision and recall scores for surplus energy prediction are 77% and 83%, respectively, indicating that the model effectively identifies true surplus energy instances while minimizing false negatives.

## References

- [British Gas - Average Energy Bill](https://www.britishgas.co.uk/energy/guides/average-bill.html)
- [SunBase Data - Solar Panel Output Calculation](https://www.sunbasedata.com/blog/how-to-calculate-solar-panel-output)
- [Wind Turbine Energy Calculation](https://x-engineer.org/wind-turbine-energy/)
