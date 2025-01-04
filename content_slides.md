# Winning Space Race with Data Science


# Executive Summary

* Summary of methodologies
* Summary of all results


# Introduction

* Project background and context
* Problems you want to find answers


# Methodology

## Methodology

Executive Summary:

* Data collection methodology:
	* Describe how data was collected 
* Perform data wrangling
	* Describe how data was processed
* Perform exploratory data analysis (EDA) using visualization and SQL
* Perform interactive visual analytics using Folium and Plotly Dash
* Perform predictive analysis using classification models
	* How to build, tune, evaluate classification models


1.	Data Collection:
	* REST API: Data from SpaceX endpoint api.spacexdata.com/v4/launches/past with additional data from /rockets, /payloads, and /launchpads.
	* Web Scraping: HTML tables from Falcon 9 Wiki pages cleaned and integrated into pandas dataframes.
2.	Data Wrangling:
	* Filtered out Falcon 1 launches to focus on Falcon 9.
	* Replaced missing PayloadMass values with the mean.
3.	Exploratory Data Analysis (EDA):
	* Visualized data with bar charts, pie charts, scatter plots, and SQL queries for trends and relationships.
4.	Interactive Visual Analytics:
	* Folium: Interactive maps with launch site markers, radii, and trajectories.
	* Plotly Dash: Dashboard for filtering by launch sites, payload mass, and visualizing success rates.
5.	Predictive Analysis:
	* Built classification models to predict landing outcomes.
	* Tuned models using GridSearchCV and evaluated with accuracy and F1-score.
6.	Model Selection:
	* Compared models via cross-validation.
	* Visualized accuracy and selected the best-performing model using confusion matrix analysis.

## Data Collection

Describe how data sets were collected:

1. SpaceX REST API:
	* Endpoint: [api.spacexdata.com](https://api.spacexdata.com/v4/launches/past)
	* This endpoint provided structured data about past SpaceX launches, including details about rockets, payloads, launchpads, and more. The data was retrieved in JSON format.
	* Supplementary data was gathered by querying additional API endpoints (e.g., /rockets, /launchpads, /payloads) to enrich and clarify key fields.
2. Web Scraping:
	* HTML tables containing Falcon 9 launch data were extracted from relevant Wiki pages using Python’s BeautifulSoup library.
	* These tables were parsed, cleaned, and converted into pandas dataframes for integration with the API data.


You need to present your data collection process use key phrases and flowcharts

### Flowchart

1. Start
1. Fetch Launch Data from API (Get Request)
1. Parse JSON Response
1. Normalize JSON Data to Flat Table (pandas)
1. Supplement Data:
	* Query Additional API Endpoints
	* Web Scrape Wiki Tables
1. Clean & Transform Data:
	* Filter Falcon 1 Launches
	* Handle Missing Values
1. Merge API and Web Scraped Data
1. Store Cleaned Dataset for Analysis
1. End

### Key Phrases

1.	REST API Access:
	* “Data was retrieved using requests library with a GET method to the endpoint api.spacexdata.com/v4/launches/past.”
	* “Supplementary data fields (e.g., rocket, payload) were enriched using targeted API calls to /rockets, /launchpads, and /payloads.”
2.	JSON Parsing and Normalization:
	* “Structured JSON responses were flattened into a tabular format using json_normalize.”
	* “Nested attributes were extracted and converted into separate columns for easier analysis.”
3.	Web Scraping:
	* “HTML tables from Falcon 9-related Wiki pages were extracted and parsed using the BeautifulSoup library.”
	* “Raw scraped data was cleaned and converted into pandas dataframes for integration.”
4.	Data Cleaning:
	* “Irrelevant records (Falcon 1 launches) were filtered out using conditional filtering in pandas.”
	* “NULL values in the PayloadMass column were replaced with the column mean for consistency.”
5.	Data Integration:
	* “The API and scraped data were merged to form a comprehensive dataset for analysis.”
	* “Unique identifiers (e.g., rocket IDs) were used to map and link data across different sources.”


## Data Collection – SpaceX API

### Key Phrases for SpaceX REST API Calls

1.	Initiate API Calls:
	*	“Used the requests library to perform GET requests on the SpaceX REST API endpoint: https://api.spacexdata.com/v4/launches/past.”
	*	“Fetched launch data, including rocket details, payload, and launch outcomes.”
2.	Parsing API Responses:
	*	“Parsed JSON responses from the API using the json() method.”
	*	“Extracted nested data for detailed analysis (e.g., rocket IDs, payload information).”
3.	Data Normalization:
	*	“Utilized pandas.json_normalize to flatten nested JSON structures into tabular format.”
	* “Mapped IDs (e.g., rockets, payloads) to descriptive details by querying supplementary API endpoints.”
4.	Data Cleaning:
	* “Filtered data to exclude Falcon 1 launches, focusing exclusively on Falcon 9.”
	* “Handled missing values in key columns like PayloadMass by replacing them with the column’s mean.”
5.	Storing Data:
	* "Prepared a clean and structured dataset for analysis and visualization.”

### Flowchart

1. Start
1. Perform GET Request to SpaceX API
	* Endpoint: /launches/past
1. Parse JSON Response
	* Use: response.json()
1. Normalize JSON Data
	* Use: pandas.json_normalize()
1. Enrich Data by Querying Additional Endpoints
	* /rockets
	* /payloads
	* /launchpads
1. Clean Data
	* Filter Falcon 1 Launches
	* Handle Missing Values (e.g., PayloadMass)
1. Store Final Dataset
1. End

### GitHub

GitHub URL: [Notebook File](https://github.com/xsagti/IBM-Applied-Data-Science-Capstone/blob/6d38cf26b8f57d254a716bfc8feb421ff724f103/Notebooks/1-jupyter-labs-spacex-data-collection-api-v2.ipynb)

## Data Collection - Scraping


### Key Phrases for Web Scraping Process

1.	Target Data Source:
	* “The target webpage is https://en.wikipedia.org/wiki/List_of_Falcon_9_and_Falcon_Heavy_launches.”
	* “HTML tables containing launch records were identified as the main source of data.”
2.	Scraping with BeautifulSoup:
	* “The requests library was used to fetch the HTML content of the webpage.”
	* “BeautifulSoup parsed the HTML content to locate relevant \<table> elements.”
3.	Extracting Table Data:
	* “Iterated over the rows of the identified table to extract data into lists or dictionaries.”
	* “Specific columns, such as launch date, payload, and outcome, were extracted for analysis.”
4.	Data Cleaning and Transformation:
	* “Converted raw table data into a pandas dataframe for further processing.”
	* “Cleaned up missing or irrelevant values, ensuring consistency in the dataset.”
5.	Data Integration:
	* “The scraped data was integrated with data from the SpaceX API to create a comprehensive dataset.”


### Flowchart

1. Start
1. Fetch HTML Content of Wikipedia Page
	* Use: requests.get()
1. Parse HTML with BeautifulSoup
	* Use: BeautifulSoup()
1. Locate and Extract Relevant Tables
	* Target: \<table> tags
1. Transform Table Data into Pandas DataFrame
	* Use: pandas.DataFrame()
1. Clean and Process Data
	* Handle Missing Values
	* Filter Irrelevant Rows
1. Integrate with API Data
2. Store Cleaned Dataset
1. End

### GitHub

GitHub URL: [Notebook file](https://github.com/xsagti/IBM-Applied-Data-Science-Capstone/blob/6d38cf26b8f57d254a716bfc8feb421ff724f103/Notebooks/2-jupyter-labs-webscraping.ipynb)


## Data Wrangling

### Key Phrases for Data Wrangling Process

1.	Data Exploration:
	* “Explored data to identify patterns and inconsistencies.”
	* “Examined outcomes such as True Ocean, False Ocean, True RTLS, False RTLS, True ASDS, and False ASDS to understand success and failure cases.”
2.	Data Transformation:
	* “Converted landing outcomes into binary labels: 1 for successful landings and 0 for unsuccessful ones.”
	* “Extracted meaningful columns for machine learning, focusing on landing success and other significant features.”
3.	Handling Missing Data:
	* “Identified and addressed null values in critical columns, replacing them with appropriate substitutes like the mean or mode.”
4.	Feature Engineering:
	* “Created new features from existing data to enhance predictive modeling, such as categorizing outcomes or normalizing numeric columns.”
5.	Integration and Storage:
	* “Integrated cleaned and transformed data into a final dataset, ready for analysis or training supervised models.”

### Flowchart

1. Start
   |
   v
2. Load Dataset
       Use: pandas.read_csv()
   |
   v
3. Perform Exploratory Data Analysis (EDA)
       - Identify key features and missing values
       - Analyze patterns in outcomes
   |
   v
4. Transform Data
       - Convert outcomes to binary labels
       - Normalize numeric columns
   |
   v
5. Handle Missing Values
       - Replace nulls with mean, median, or mode
   |
   v
6. Feature Engineering
       - Create derived features
       - Categorize or encode key columns
   |
   v
7. Save Processed Dataset
       Use: pandas.to_csv()
   |
   v
8. End

### GitHub

GitHub URL: [Notebook File](https://github.com/xsagti/IBM-Applied-Data-Science-Capstone/blob/6d38cf26b8f57d254a716bfc8feb421ff724f103/Notebooks/3-jupyter-labs-spacex-Data%20wrangling-v2.ipynb)



## EDA with Data Visualization

* Summarize what charts were plotted and why you used those charts
* Add the GitHub URL of your completed EDA with data visualization notebook, as an external reference and peer-review purpose

### Charts Plotted and Their Purpose

1.	Bar Charts:
	* Why: To visualize categorical distributions, such as the number of successful vs. unsuccessful landings or the frequency of launch sites.
	* Example: A bar chart showing the count of launches by launch site to identify the most frequently used sites.
2.	Pie Charts:
	* Why: To display proportions, such as the percentage of launches that succeeded or failed.
	* Example: A pie chart illustrating the success rate of Falcon 9 landings.
3.	Scatter Plots:
	* Why: To analyze relationships between numerical variables, such as payload mass and landing outcome.
	* Example: A scatter plot showing payload mass versus success rate to identify trends.
4.	Histograms:
	* Why: To display distributions of continuous variables, such as payload mass.
	* Example: A histogram of payload mass to identify common payload sizes.
5.	Box Plots:
	* Why: To analyze data variability and detect outliers.
	* Example: A box plot of payload mass grouped by success or failure to understand variability in payload sizes.
6.	Line Charts:
	* Why: To observe trends over time, such as the number of successful launches per year.
	* Example: A line chart showing the trend of successful landings over time.

### GitHub

GitHub URL: [Notebook File](https://github.com/xsagti/IBM-Applied-Data-Science-Capstone/blob/6d38cf26b8f57d254a716bfc8feb421ff724f103/Notebooks/5-jupyter-labs-eda-dataviz-v2.ipynb)


## EDA with SQL


### Summary of SQL Queries

1. Data Ingestion:
	* “Loaded the SpaceX dataset into a database table using CSV import methods.”
	* “Verified successful data ingestion with SELECT COUNT(*) and table structure inspection.”
2. Basic Exploration:
	* “Queried the first few rows of the table using SELECT * FROM table_name LIMIT n.”
	* “Checked unique values for key fields like LaunchSite using SELECT DISTINCT column_name.”
3. Aggregations:
	*	“Calculated the total number of launches per launch site using GROUP BY and COUNT().”
	* “Summarized the success rate of landings with COUNT and CASE statements.”
4. Filtering and Conditions:
	* “Filtered records for specific rockets (e.g., Falcon 9) using WHERE conditions.”
	* “Queried payload data for launches exceeding a specified mass using WHERE payload_mass > value.”
5. Joins:
	* “Joined tables to enrich launch data with additional details, such as rocket or payload information.”
	* “Used INNER JOIN for integrating related datasets based on unique identifiers.”
6. Sorting:
	* “Ranked launches by payload mass using ORDER BY payload_mass DESC to identify the heaviest payloads.”

### GitHub

GitHub URL: [Notebok File](https://github.com/xsagti/IBM-Applied-Data-Science-Capstone/blob/6d38cf26b8f57d254a716bfc8feb421ff724f103/Notebooks/4-jupyter-labs-eda-sql-coursera_sqllite.ipynb)


## Build an Interactive Map with Folium


### Summary of Map Objects Added

1.	Markers:
	* Purpose:
		* Highlight specific launch site locations on the map.
		* Provide information about each launch site (e.g., name and location) through popups.
	* Why:
		* Helps visualize where each launch site is geographically located.
2.	Circles:
	* Purpose:
		* Represent the radius around each launch site to analyze proximity-related factors (e.g., population density or water bodies).
	* Why:
		* Useful for understanding spatial relationships and their potential impact on launch outcomes.
3.	Lines:
	* Purpose:
		* Draw trajectories from launch sites to target locations in orbit or highlight distances between locations.
	* Why:
		* Provides a visual representation of launch trajectories and geographic context.
4.	Layers:
	* Purpose:
		* Use additional map layers (e.g., satellite view or terrain view) to analyze geographic features.
	* Why:
		* Offers diverse perspectives for understanding environmental and geographic impacts.


### GitHub

GitHub URL: [Notebook File](https://github.com/xsagti/IBM-Applied-Data-Science-Capstone/blob/6d38cf26b8f57d254a716bfc8feb421ff724f103/Notebooks/6-jupyter-labs-launch-site-location-v2.ipynb)


## Build a Dashboard with Plotly Dash


### Plots/Graphs and Interactions

1.	Scatter Plot:
	* Purpose: Visualizes the relationship between payload mass and launch success for different launch sites.
	* Interactions:
		* Dropdown to filter data by specific launch sites or show all sites.
		* Dynamic updates based on user selection.
	* Why:
		* Helps identify patterns or correlations between payload and launch success across sites.
2.	Pie Chart:
	* Purpose: Displays the success rate of launches for selected launch sites.
	* Interactions:
		* Dropdown to select a specific launch site or view aggregated data for all sites.
	* Why:
		* Offers a clear and intuitive representation of success rates, making it easy to compare performance.
3.	Range Slider for Payload Mass:
	* Purpose: Allows users to filter data by payload mass range.
	* Interactions:
		* Adjusting the slider dynamically updates the scatter plot to reflect the selected payload range.
	* Why:
		* Enables detailed exploration of the impact of payload mass on launch success.
4.	Dynamic Layout:
	* Purpose: Organizes the dashboard with interactive components and visualizations for a seamless user experience.
	* Why:
		* Ensures that all interactions and plots are accessible and visually appealing.

### Why These Plots and Interactions Were Added

* To facilitate interactive exploration of SpaceX launch data.
* To provide insights into key performance metrics, such as payload effects and success rates.
* To make the analysis user-friendly and visually compelling through dynamic updates and customizable filters.


### GitHub

GitHub URL: [Notebook File](https://github.com/xsagti/IBM-Applied-Data-Science-Capstone/blob/6d38cf26b8f57d254a716bfc8feb421ff724f103/Notebooks/7-python-spacex_dash_app.py)


## Predictive Analysis (Classification)


### Model Development Process

1.	Data Preparation:
	* Selected key features (payload mass, orbit, launch site, booster version).
	* Encoded categorical variables (e.g., one-hot encoding).
	* Normalized numerical values for uniform scaling.
2.	Model Building:
	* Tested models: Logistic Regression, Decision Trees, SVM, KNN, and Random Forests.
3.	Model Evaluation:
	* Metrics: Accuracy, Precision, Recall, F1-Score.
	* Applied cross-validation for robustness.
4.	Hyperparameter Tuning:
	* Used GridSearchCV to optimize key parameters (e.g., C for Logistic Regression, max_depth for Decision Trees).
5.	Best Model Selection:
	* Chose the model with the highest F1-Score and cross-validation performance.
6.	Final Testing:
	* Validated on unseen test data and analyzed the confusion matrix.

### Flowchart

1. Start
   |
   v
2. Load and Preprocess Data
       - Encode categorical features
       - Normalize numerical values
   |
   v
3. Train Models
       - Logistic Regression
       - Decision Trees
       - SVM
       - KNN
       - Random Forests
   |
   v
4. Evaluate Models
       - Accuracy, Precision, Recall
       - F1-Score
       - Cross-validation
   |
   v
5. Tune Hyperparameters
       - Use GridSearchCV for optimization
   |
   v
6. Select Best Model
       - Based on evaluation metrics
   |
   v
7. Final Testing
       - Evaluate on unseen test data
       - Generate confusion matrix
   |
   v
8. End

### GitHub

GitHub URL: [Notebook File](https://github.com/xsagti/IBM-Applied-Data-Science-Capstone/blob/6d38cf26b8f57d254a716bfc8feb421ff724f103/Notebooks/8-jupyter-labs-SpaceX-Machine-Learning-Prediction-Part-5-v1.ipynb)


## Results

* Exploratory data analysis results
* Interactive analytics demo in screenshots
* Predictive analysis results


# Section 2 - Insights drawn from EDA

## Flight Number vs. Launch Site


![Relationship between Flight Number and Launch Site](Images/EDA with Data Visualization - scatter plot - relationship between Flight Number and Launch Site.png)

### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.


## Payload vs. Launch Site

![Relatinship between Payload and Launch Site](Images/EDA with Data Visualization - scatter plot - relationship between Payload and Launch Site.png)

### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.


## Success Rate vs. Orbit Type

![Relationship between Success/Failure rate and Orbit](Images/EDA with Data Visualization - scatter plot - relationship between success rate of each orbit type.png)

### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.


## Flight Number vs. Orbit Type

![Relationship between Flight Number and Orbit](Images/EDA with Data Visualization - scatter plot - relationship between FlightNumber and Orbit type.png)

### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.


## Payload vs. Orbit Type

![Relationship between Payload and Orbit](Images/EDA with Data Visualization - scatter plot - relationship between Payload and Orbit type.png)

### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.


## Launch Success Yearly Trend

![Launch Success Yearly Trend](Images/EDA with Data Visualization - line plot - launch success yearly trend.png)

### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.


## All Launch Site Names


```SQL
SELECT 
	distinct Launch_Site
FROM
	SPACEXTABLE
```

| Launch_Site |
|----|
|CCAFS LC-40
|VAFB SLC-4E
|KSC LC-39A
|CCAFS SLC-40

| Launch Site | Lat | Long |
|---|---|---|
| CCAFS LC-40 | 28.562302 | -80.577356 |
| CCAFS SLC-40 | 28.563197 | -80.576820 |
| KSC LC-39A | 28.573255 | -80.646895 |
| VAFB SLC-4E | 34.632834 | -120.610745 |

### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

## Launch Site Names Begin with 'CCA'


```SQL
SELECT
	*
FROM 
	SPACEXTABLE 
WHERE 
	Launch_Site like 'CCA%' limit 5
```

![Launch Site Names Begin with CCA](Images/SQL - Launch Site Names Begin with CCA.png)


### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.


## Total Payload Mass


```SQL
SELECT
	SUM(PAYLOAD_MASS__KG_) as TOTAL_PAYLOAD_MASS_KG_ 
FROM 
	SPACEXTABLE 
WHERE 
	Customer = 'NASA (CRS)'
```

| TOTAL\_PAYLOAD\_MASS\_KG\_|
|----|
|45596|


### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

## Average Payload Mass by F9 v1.1


```SQL
SELECT
	AVG(PAYLOAD_MASS__KG_) as AVG_PAYLOAD_MASS_KG_ 
FROM 
	SPACEXTABLE 
WHERE 
	Booster_Version LIKE 'F9 v1.1%'

```

|AVG\_PAYLOAD\_MASS\_KG\_|
|----|
|2534.6666666666665|


### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.


## First Successful Ground Landing Date

```SQL
SELECT 
	Date 
FROM
	SPACEXTABLE 
WHERE 
	Landing_Outcome LIKE 'Success%' order by Date asc limit 1
```

|Date|
|----|
|2015-12-22|


### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

## Successful Drone Ship Landing with Payload between 4000 and 6000


```SQL
SELECT 
	Booster_Version 
FROM 
	SPACEXTABLE 
WHERE 
	Landing_Outcome == 'Success (drone ship)' and PAYLOAD_MASS__KG_ > 4000 and PAYLOAD_MASS__KG_ < 6000

```

| Booster_Version |
|---|---|
| F9 FT B1022 |
| F9 FT B1026 |
| F9 FT B1021.2 |
| F9 FT B1031.2 |

### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.


## Total Number of Successful and Failure Mission Outcomes


```SQL
SELECT 
	Mission_Outcome, 
	COUNT(*) as Count 
FROM 
	SPACEXTABLE 
GROUP BY 
	Mission_Outcome
```

| Mission_Outcome | Count |
|---|---|
| Failure (in flight) | 1 |
| Success | 98 |
| Success | 1 |
| Success (payload status unclear) | 1  | 


### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

```SQL
SELECT 
	COUNT(*) 
FROM 
	SPACEXTABLE 
WHERE 
	Landing_Outcome LIKE 'Success%' 
```


| Success COUNT (*) |
|---|
| 61 |


### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

```SQL
SELECT 
	COUNT(*) 
FROM 
	SPACEXTABLE 
WHERE 
	Landing_Outcome LIKE 'Failure%' 
```

| Failure COUNT (*) |
|---|
| 10 |


### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.


```SQL
SELECT 
    COUNT(CASE WHEN Landing_Outcome LIKE 'Success%' THEN 1 END) AS SuccessCount, 
    COUNT(CASE WHEN Landing_Outcome LIKE 'Failure%' THEN 1 END) AS FailureCount 
FROM 
	SPACEXTABLE;
```

| Success | Failures |
|---|---|
| 61 | 10 |


### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.


## Boosters Carried Maximum Payload


```SQL
SELECT 
	DISTINCT Booster_Version
FROM 
	SPACEXTABLE
WHERE 
	PAYLOAD_MASS__KG_ = (SELECT MAX(PAYLOAD_MASS__KG_) FROM SPACEXTABLE)
```

| Booster_Version |
|---|---|
| F9 B5 B1048.4 |
| F9 B5 B1049.4 |
| F9 B5 B1051.3 |
| F9 B5 B1056.4 |
| F9 B5 B1048.5 |
| F9 B5 B1051.4 |
| F9 B5 B1049.5 |
| F9 B5 B1060.2 |
| F9 B5 B1058.3 |
| F9 B5 B1051.6 |
| F9 B5 B1060.3 |
| F9 B5 B1049.7 |

### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.


## 2015 Launch Records


```SQL
SELECT 
	substr(Date, 6,2) as month,
    Landing_Outcome,
    Booster_Version,
    Launch_Site
FROM 
	SPACEXTABLE
WHERE 
	substr(Date,0,5)='2015'
	AND 
	Landing_Outcome like 'Failure (drone ship)'
ORDER 
	BY month;
```

| Month | Landing_Outcome | Booster_Version | Launch_Site |
|---|---|---|---|
| 01 | Failure (drone ship) | F9 v1.1 B1012 | CCAFS LC-40 |
| 04 | Failure (drone ship) | F9 v1.1 B1015 | CCAFS LC-40 |


### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.


## Rank Landing Outcomes Between 2010-06-04 and 2017-03-20


```SQL
SELECT
    Landing_Outcome,
    COUNT(Landing_Outcome) as Count
FROM 
	SPACEXTABLE
WHERE 
	Date BETWEEN '2010-06-04' AND '2017-03-20'
GROUP BY 
	Landing_Outcome
ORDER BY 
	Count DESC 
```

| Landing_Outcome | Count |
|---|---|
| No attempt       | 10    |
| Success (drone ship) | 5     |
| Failure (drone ship) | 5     |
| Success (ground pad) | 3     |
| Controlled (ocean) | 3     |
| Uncontrolled (ocean) | 2     |
| Failure (parachute) | 2     |
| Precluded (drone ship) | 1     | 

### Explanations
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.


# Section 3 - Launch Sites Proximities Analysis


## Folium Map - All Launch Sites

Datasourece: spacex\_launch_geo.csv

![All Launches](Images/FOLIUM - Task 1 - Mark all launch sites on a mpa.png)


| Launch Site | Lat      | Long      |
|-------------|---------|---------|
| CCAFS LC-40  | 28.562302 | -80.577356 |
| CCAFS SLC-40 | 28.563197 | -80.576820 |
| KSC LC-39A   | 28.573255 | -80.646895 |
| VAFB SLC-4E  | 34.632834 | -120.610745 |


### Explanations
Explain the important elements and findings on the screenshot




## Folium Map - Success/Failed launches for site 

![](Images/FOLIUM - Task 2 - Mark the success launches for each site on the map - 1.png)

![](Images/FOLIUM - Task 2 - Mark the success launches for each site on the map - 2.png)

### Explanations
Explain the important elements and findings on the screenshot


## Folium Map - Distance from launch site to proximities

![Distance from launch site to proximities](Images/FOLIUM - Task 3 - distances between a launch site to its proximities.png)

### Explanations
Explain the important elements and findings on the screenshot


# Section 4 - Build a Dashboard with Plotly Dash


## Dashboard Screenshot 1

![Dashboard Screenshot 1](Images/Dashboard Screenshot 1.png)

### Explanations
Explain the important elements and findings on the screenshot

## Dashboard Screenshot 2

![Dashboard Screenshot 2](Images/Dashboard Screenshot 2.png)


### Explanations
Explain the important elements and findings on the screenshot

## Dashboard Screenshot 3


![Dashboard Screenshot 3](Images/Dashboard Screenshot 3.png)
![Dashboard Screenshot 3 - 2](Images/Dashboard Screenshot 3 - 2.png)


### Explanations
Explain the important elements and findings on the screenshot, such as which payload range or booster version have the largest success rate, etc.

# Section 5 - Predictive Analysis (Classification)

## Classification Accuracy


* Find which model has the highest classification accuracy

![Classification Model Test Accuracies](Images/Predictive Analysis - Classification Model Test Accuracies.png)

| Modelo             | Exactitud de Prueba |
|--------------------|--------------------|
| LogisticRegression | 0.8333             |
| SVM                | 0.8333             |
| DecisionTree       | 0.8333             |
| KNN                | 0.8333             |


### Explanation

* Find which model has the highest classification accuracy

## Confusion Matrix

![Confusion Matrix](Images/Predictive Analysis - Confussion Matrix.png)

### Explanation
how the confusion matrix of the best performing model with an explanation

## Conclusions

* Point 1
* Point 2
* Point 3
* Point 4
* ...


## Appendix

- Include any relevant assets like Python code snippets, SQL queries, charts, Notebook outputs, or data sets that you may have created during this project
    




