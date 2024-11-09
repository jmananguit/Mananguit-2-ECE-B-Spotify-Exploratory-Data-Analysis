# <img src="https://github.com/user-attachments/assets/3b37ec7c-df47-4ca1-9bed-d0ada09d9c91" alt="Spotify_Primary_Logo_RGB_Green" width="40" height="40"> Spotify 2023 Exploratory Data Analysis
A short summary and analysis on the 2023 Spotify Most Streamed Songs Created by Nidula Elgiriyewithana.

:pushpin:Source: https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023
# :question: About 
This project aims to explore the dataset using python and provide the summary and statistics to give overview or insights. 
At the end of this project it is expected to:
- Extract data from the dataset using python
- Provide visualizations of data using python
- Intepret the data gathered and provide insights about the data

# :page_facing_up: Code Documentation 
## Importing Needed Libraries
The following are the libraries used in the code:
- Numerical Python
- Matplotlib
- Python Data Analysis
- Seaborn
> :exclamation: Note: Import all libraries at the start of the code to improve code readability and prevent import issues
```python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
```
# Overview of Dataset
## Importing the dataset
> :exclamation:The Spotify Dataset Used in this project is also uploaded in this repository

To import the CSV file, use ```python pd.load_csv()``` 
``` python
dataset = pd.read_csv('SpotifyData2023.csv')
dataset
```
- Throughout this code the variable name 'dataset' will be used to refer original csv file
## Determining the number of rows and columns
Use the ```.shape()``` command in order get the values of its rows and columns 
``` python
#Obtain the number of rows and columns from the dataset and assign it to a variable
rows, columns = dataset.shape
#Print the number of Rows and Columns
print('Number of Rows:',rows)
print('Number of Columns:',columns)
```
#### Expected Result
```python
Number of Rows: 953
Number of Columns: 24
```

## Determining the Missing Values and Data Types
### Missing Values
- In order to calculate the count of missing values for each column in the dataset, we need to determine the total number of NaN (Not a Number) elements in the dataset
- The command '.isnull' can be used to determine if an elemenet in a dataframe is NaN
### :exclamation: Data Type Issue
- By observing the given spotify csv file, it can be seen that at the column 'streams' there is one data which is a string
 <div align="center">
 <img src="https://github.com/user-attachments/assets/7cb94ed8-312c-4eaa-bb16-1e5f4f74c0a3" alt="Spotify CSV observation" width="500" height="300">
  </div>
  
- To properly count number of Missing Values, change the string into a NaN value
``` python
# Convert non-numeric values to NaN
dataset['streams'] = pd.to_numeric(dataset['streams'], errors='coerce')
# Calculate the count of missing values for each column in the dataset
missingval_count = dataset.isnull().sum().reset_index()
#Change column names for better presentation of table
missingval_count.columns=['Columns', 'Missing_Value']
# Display the missing values count and limit the number of printed results to not clutter up the terminal
print('Missing values per column:')
print('\n',missingval_count.head(10))
```
#### Expected Result 
<div align="center">
  <img src="https://github.com/user-attachments/assets/316807ee-2af6-4c36-91da-ab090a87f694" alt="image" width="300" height="280">
</div>
 
### Data Types
``` python
data_types = dataset.dtypes.value_counts()
#to properly change the column name without affect the data, assign data_types to another variable
data_types_table = data_types.reset_index()
#Rename columns
data_types_table.columns = ['Data Type', 'No. Col']
#print the table
print('Number of Columns per data type:')
data_types_table
```

