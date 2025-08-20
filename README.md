# top-secret
Irrigation Management System Code
This project contains Python code for an irrigation management system that calculates crop water requirements, predicts irrigation needs, and visualizes key data for effective agricultural planning.

1. Installation
To run this code, you'll need the following Python libraries. You can install them using pip:

Bash

pip install pandas numpy matplotlib seaborn scikit-learn
2. Code Breakdown
The code is organized into several key sections, each handling a specific part of the irrigation management process.

Data Loading and Setup
This section imports necessary libraries and sets up a sample pandas DataFrame containing mock weather data for a week. The data includes daily maximum and minimum temperatures, humidity, solar radiation, and rainfall.

Core Calculations: Evapotranspiration
The system calculates two important metrics:

Reference Evapotranspiration (ET_0): This is the potential water loss from a reference crop. The code uses the Hargreaves equation to estimate ET_0 based on temperature and solar radiation.
$ET\_0 = 0.0023 \* (T\_{max} - T\_{min})^{0.5} \* (T\_{max} + T\_{min}) / 2 \* R\_a$

Crop Evapotranspiration (ET_c): This is the actual water requirement of a specific crop. It's calculated by multiplying the ET_0 by a crop coefficient (K_c), which accounts for the crop type and its growth stage.
$ET\_c = ET\_0 \* K\_c$

Irrigation Requirement Calculation
This step determines the daily net irrigation by subtracting the day's rainfall from the crop's water need (ET_c). The result is capped at zero, as you can't have negative irrigation.

net_irrigation = max(ET_c - rainfall, 0)

Predictive and Scheduling Features
Machine Learning Model: A Random Forest Regressor is trained on historical data to predict future irrigation needs, enabling proactive management.

Irrigation Schedule: A function calculates the total water volume in liters required for a given field area based on the daily net irrigation value.

Soil Moisture Check: A simple function simulates a soil moisture sensor and recommends irrigation if the moisture level drops below a set threshold.

3. Data Visualization and Reporting
The code generates various plots and reports to help visualize and analyze the data:

Line and Bar Charts: Plots are created to show the relationship between crop water demand (ET_c), rainfall, and the resulting irrigation need over a week.

Water Balance Report: A summary report provides the total weekly crop demand, rainfall, and irrigation required, giving a clear overview of the water balance.

Daily Report: A detailed, day-by-day printout shows all calculated values (ET_0, ET_c, rainfall) and the final irrigation recommendation.

Heatmap: A heatmap visualizes irrigation requirements over multiple weeks, helping to identify patterns and trends.

4. Advanced Data Analysis (Weather Data & Plant Sensor Data)
The latter part of the code demonstrates more advanced data analysis techniques:

Reading and Plotting Weather Data: The script reads a Weather Data.csv file, cleans the data, and generates multiple plots, including a box plot of temperature, a scatter plot of temperature vs. dew point, and histograms and bar charts of wind speed and weather conditions. This provides a comprehensive statistical view of the weather data.

Analyzing Plant Sensor Data: The code reads and merges data from three separate CSV files (plant_vase1.CSV, plant_vase1(2).CSV, plant_vase2.CSV) to analyze soil moisture over time. It cleans and processes the data by:

Combining date and time columns into a single timestamp.

Creating a new column for the average moisture across all sensors.

Plotting the average moisture level over time alongside a critical irrigation threshold. This plot visually indicates when the soil moisture dropped below the required level.

Automated Recommendation: A function uses the processed sensor data to provide a real-time irrigation recommendation based on the most recent moisture reading, simulating a smart irrigation system.
