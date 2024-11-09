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
```
``` python
#Print the number of Rows and Columns
print('Number of Rows:',rows)
print('Number of Columns:',columns)
```
#### Expected Result:
```python
Number of Rows: 953
Number of Columns: 24
```

## :part_alternation_mark: Determining the Missing Values and Data Types
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
dataset['streams'] = pd.to_numeric(dataset['streams'], errors='coerce')
```
- Calculate the count of missing values for each column in the dataset
``` python
missingval_count = dataset.isnull().sum().reset_index()
```
- Change column names for better presentation of table
``` python
missingval_count.columns=['Columns', 'Missing_Value']
```
- Display the missing values count and limit the number of printed results to not clutter up the terminal
``` python
print('Missing values per column:')
print('\n',missingval_count.head(10))
```
#### Expected Result 
<div align="center">
  
    Missing values per column:
    
                     Columns  Missing_Value
    0            track_name              0
    1        artist(s)_name              0
    2          artist_count              0
    3         released_year              0
    4        released_month              0
    5          released_day              0
    6  in_spotify_playlists              0
    7     in_spotify_charts              0
    8               streams              1
    9    in_apple_playlists              0

</div>

## Basic Plotting Commands
- These Commands are Essential in Order to Properly Visualize the Data we Gathered

``` python
sns.barplot() - Creates a barplot of the given data
sns.lineplot() - Creates a lineplot
plt.title() - Creates the title of the plot
plt.figure(figsize=(x,y)) - Determines the canvas size of the plot
plt.xticks() - Rotates the text of the x and y data
plt.xlabel - Creates Label for X Axis
plt.ylabel - Creates Label for Y Axis
plt.legend() - Creates Legend
plt.show() - Prints the plot
```
### Missing Values Plot

- Calculate the sum of missing values (NaN) for each column in the dataset
``` python
missingval_count = dataset.isnull().sum()
```
- Create a new figure with specified size 
``` python
plt.figure(figsize=(12, 6))
```
- Create a bar plot using seaborn
  - x-axis: column names from the dataset
  - y-axis: count of missing values
  - palette: "viridis" color scheme
  - hue: color intensity based on missing value count
    
``` python
sns.barplot(x=missingval_count.index, y=missingval_count.values, palette="viridis",hue=missingval_count)
```
- Customize the format of the plot and add titles
``` python
plt.title('Missing Values per Column')
plt.xticks(rotation=90)
plt.xlabel('Column Names')
plt.ylabel('Missing Values')
plt.legend(title='Missing Values')
plt.show()
```
#### Expected Result:
<div align="center">
<img src="https://github.com/user-attachments/assets/45fa9f61-1c7a-4541-bfac-ef5f6c6c6d47"alt="image" width="600" height="350">
</div>

### Data Types
- To determine data types, the command ```python .dtypes ``` can be used.
- To calculate the number of columns with each data type, the command ```python .value_counts ``` can be used
-Syntax: varname = dataFrame.dtypes.valuecounts()
``` python
data_types = dataset.dtypes.value_counts()
```
- To properly change the column name without affect the data, assign data_types to another variable
``` python
data_types_table = data_types.reset_index()
```
- Rename columns
``` python
data_types_table.columns = ['Data Type', 'No. Col']
```
- Print the table
``` python
print('Number of Columns per data type:')
data_types_table
```
#### Expected Result

<div align="center">
<img src="https://github.com/user-attachments/assets/e812f99c-6d5c-4523-b8be-cd37913c059c">
</div>

### Data Type Plot
> :exclamation: Use the Plotting Commands Shown Earlier

- Set figure with specified size 
```python
plt.figure(figsize=(8, 6))
```
- Create barplot using seaborn
```python
sns.barplot(x=data_types.index.astype(str), y=data_types.values, palette="viridis",hue=data_types.index.astype(str))
```
- Customize the format of the plot and add titles
```python
plt.title("Number of Each Data Type in Dataset")
plt.xlabel("Data Type")
plt.ylabel("Count of Columns")
plt.xticks(rotation=45)
plt.show()
```

#### Result

<div align="center">
<img src="https://github.com/user-attachments/assets/b127bf52-89c4-4594-9121-1128ac60e3eb">
</div>

### Data Type for Each Column
- To get the data type for Each Column the following will be used
- '.dtypes()' - returns data type of each column
- .reset_index() - used to properly format the table
  
- Determine the the data type for each column and assign to a variable
``` Python
column_data_types = dataset.dtypes.reset_index()
```
- Renames the columns of column_data_types
``` Python
column_data_types.columns = ['Column', '   Data Type']
```
- Display the DataFrame with column names and their data types
``` Python
print("\nData types of each column:") 
column_data_types
```
#### Expected Result
<p align="center">
  <img src="https://github.com/user-attachments/assets/3a909c98-20cb-4604-b717-3fcba4352d44" width="36%" alt="Image 1">
  <img src="https://github.com/user-attachments/assets/9184fe8e-0a1e-4af4-abae-e0b6562ae304" width="36%" alt="Image 2">
</p>

## Data Wrangling

- To properly utilize the data from the spotify dataset, the data set must be manipulated in order to interpret and extract useful data
- **Problems with the Dataset**
  - **Missing Value Columns** - replace NaN values with 0 using command '.fillna()
  - **Columns with numbers** - replace values containing strings and change datatype into integers

 -  Replace missing values with 0
 ```python
dataset.fillna(0, inplace=True)  # The inplace=True modifies the DataFrame in place
```
- Replace values with commas and change data type into integer
 ```python
dataset['in_deezer_playlists'] = dataset['in_deezer_playlists'].astype(str).str.replace(',', '').fillna(0).astype(float).astype(int)
dataset['in_shazam_charts'] = dataset['in_shazam_charts'].astype(str).str.replace(',', '').fillna(0).astype(float).astype(int)
```
# 🔴Summary and Insights of Overview of Dataset
:purple_circle: In total it was found that the number of rows in the dataset was found to be 953 rows and the total number of columns was found to be 24. In addition the dataset was found to have three data types which include integers, floats, and strings. After looking at the dataset, it was also found that there are a number of missing values. Based on the data, the column with highest number of missing value was 'keys', followed by 'in_shazam_charts'. With relation to this the highest amount of missing data type as integers which corresponds to the high number of missing 'in_shazam_charts' values then followed by strings. 

❗ In addition, to improve compatibility of the dataset, you might have to convert the file type in order to be properly called within the python code.
## Basic Descriptive Statistics

- **Commands Used**
  - **'.mean()'** - finds the average of the column
  - **'median()'** - finds the median of the column
  - **'.std()'** - finds the standard deviation of the column
- **Syntax**
  - varname = dataFrame.iloc[col].stat_command()
    - **'.iloc'** - slicing index of 'streams' column
    - **'.stat_command()'** - use the appropriate statistical command (mean, median, std_dev)

- Calculate the mean of the 'streams' column
```python
mean = dataset.iloc[:, 8].mean()
print('The Average Number of Streams is:',mean)
```
- Calculate the median of the 'streams' column
```python
median = dataset.iloc[:, 8].median()
print('The Median of Number of Streams is:',median)
```
- Calculate the standard deviation of the 'streams' column
```python
stddev = dataset.iloc[:, 8].std()
print('The Standard Deviation of Streams is:', stddev)
```

#### Expected Output

> **The Average Number of Streams is: 513597931.3137461**

> **The Median of Number of Streams is: 290228626.0**

> **The Standard Deviation of Streams is: 566803887.0588316**


- **Number of Songs per Year**
  - **Syntax**
    - varname = dataframe['released_year'].value_counts().sort_index().reset_index()
    - **.value_counts()** - counts the occurrences of each unique value in the released_year column of dataset.
    - **.sort_index()** - sorts the results by the index
    - 
- Calculate the number of songs released per year
```python
tracks_per_year = dataset['released_year'].value_counts().sort_index().reset_index()
```
- Change column names
```python
tracks_per_year.columns=['Released_Year', 'Number of tracks']
```
- Display the result first 5 and last 5 to keep the terminal tidy
```python
print("Number of Songs per Year:")
print(tracks_per_year.head())
print(tracks_per_year.tail())
```
#### Expected Result
       Released_Year  Number of tracks
    0           1930                 1
    1           1942                 1
    2           1946                 1
    3           1950                 1
    4           1952                 1
        Released_Year  Number of tracks
    45           2019                36
    46           2020                37
    47           2021               119
    48           2022               402
    49           2023               175

- Count the number of tracks released each year
```python
tracks_per_year = dataset['released_year'].value_counts().sort_index()
```
- Plotting the line plot for the count of songs per released year
```python
plt.figure(figsize=(12, 6))
sns.lineplot(x=tracks_per_year.index, y=tracks_per_year.values, marker="o", color='b')
```
- Customize the format of the plot and add titles
```python
plt.title("Count of Tracks per Released Year")
plt.xlabel("Released Year")
plt.ylabel("Number of Tracks")
plt.xticks(rotation=45)  # Rotate x-axis labels for better readability
plt.grid(True)
plt.show()
```
#### Expected Result

<p align="center">
  <img src="https://github.com/user-attachments/assets/9730c813-a4d2-4cee-a338-091b129efcc6" alt="Centered Image">
</p>

### Number of Tracks per Artist Count

- To calculate the number of tacks per artist count, the command **<span style="background-color: #FFDFD3; color: black">'.value_counts'</span>** can be used
  - **Syntax** - varname = dataFrame[artist_count].valuecounts().sort_index().reset_index()
  - **.value_counts()** - counts the occurrences of each unique value in the released_year column of dataset.
  - **.reset_index()** - used to properly format the table

- Calculate number of tracks per number of artists
```python
artist_count_values = dataset['artist_count'].value_counts().sort_index().reset_index()
```
- Rename columns to the proper format
```python
artist_count_values.columns = ['Artist Count', 'Number of Tracks']
```
- Print Value
```python
artist_count_values
```
#### Expected Value
<p align="center">
  <img src="https://github.com/user-attachments/assets/c756ba7a-eab1-4e76-ba41-abda494490c6" alt="Centered Image">
</p>



- To properly visualize the data, a bar plot can be used
- Count the occurrences of each artist count (number of songs with a particular artist count)
```python
artist_count_values = dataset['artist_count'].value_counts().sort_index()
```
- Configure figure size
```python
plt.figure(figsize=(12, 6))
```
- Create barplot
```python
sns.barplot(x=artist_count_values.index, y=artist_count_values.values, palette="viridis",hue=artist_count_values)
```
- Customize the format of the plot and add titles
```python
plt.title("Distribution of Artist Count (Number of Track per Artist Count)")
plt.xlabel("Number of Artists per track")
plt.ylabel("Number of Tracks")
plt.legend(title='No. Tracks')
plt.show()
```
#### Expected Result
<p align="center">
  <img src="https://github.com/user-attachments/assets/836b6162-c04e-41bd-ab5a-fb40138dcc18" alt="Centered Image">
</p>

# 🔴 Summary of Basic Descriptive Statistics

🟣 The average number of streams in this dataset is approximately 513.6 million. This value indicates the central tendency of track popularity across all songs. The median number of streams, at 290.2 million, provides the midpoint of the data, showing that half of the tracks have fewer than this number of streams, while the other half have more. The standard deviation of streams is 566.8 million, reflecting substantial variability in track popularity, with some tracks significantly outperforming others in terms of stream count. This high standard deviation suggests that a few tracks might have exceptionally high stream counts, creating a wide range in the dataset. It was found that as the years passes by, the number tracks increased dramatically. Specifically, there is a big spike in the increase number of tracks starting around the year 2020. As for the Artist Count, it was found that the lesser number of Artist work on a track, the higher of number of tracks are produced. This implies that most Artists and Musicians prefers to work alone or be much more efficient in releasing tracks. 



## Top Performers

- To determine the track that has the highest number of streams, we can use **<span style="background-color: #FFDFD3; color: black">'.sort_values'</span>** command
- Sort the dataset values by streams in descending order 
```python
ascdataset = dataset.sort_values(by='streams',ascending=False)
```
- Display the top 5 most streamed tracks
```python
ascdataset = ascdataset.head(5)
```
- Slice only 'track_name', 'artist(s)_name', 'streams'
```python
ascdataset[['track_name', 'artist(s)_name', 'streams']]
```
#### Expected Result
<p align="center">
  <img src="https://github.com/user-attachments/assets/68ad3e47-02d2-45b2-b186-eb9d31e5c8b3" alt="Centered Image">
</p>


- Plotting the barplot for the top 5 most streamed tracks using Seaborn
```python
plt.figure(figsize=(10, 6))
sns.barplot(data=ascdataset, x='track_name', y='streams', palette='dark:skyblue',hue='track_name')
plt.xlabel('Track Name')
plt.ylabel('Streams')
plt.title('Top 5 Most Streamed Tracks')
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()
```
#### Expected Result
<p align="center">
  <img src="https://github.com/user-attachments/assets/a1cd7139-c218-4e9d-b49e-20fc5d692724" alt="Centered Image">
</p>

- To calculate the number of tacks per artist, the command **<span style="background-color: #FFDFD3; color: black">'.value_counts'</span>** can be used
  - **Syntax** - varname = dataFrame[artist_count].valuecounts().sort_index().reset_index()
  - **.value_counts()** - counts the occurrences of each unique value in the released_year column of dataset.
  - **.reset_index()** - used to properly format the table
  - **.sort_index()** - sorts the index of the table

- Count the occurrences of each artists' appearance
```python
topartist = dataset['artist(s)_name'].value_counts().reset_index()
topartist = topartist.head(5)
```
- rename the columns
```python
topartist.columns = ['Artist Name', 'Tracks']
```
- Print values
```python
topartist
```
#### Expected Result
<p align="center">
  <img src="https://github.com/user-attachments/assets/c2bdfe48-edee-4307-adcc-7f3e7daa7b85" alt="Centered Image">
</p>



###  Plot for Top 5 Most Frequent Artists Based on the Number of tracks

- Plotting the barplot for the top 5 most frequent artists by number of tracks using Seaborn
```python
plt.figure(figsize=(10, 6))
sns.barplot(data=topartist, x='Artist Name', y='Tracks', palette='dark:lightcoral',hue='Artist Name')
plt.xlabel('Artist Name')
plt.ylabel('Number of Tracks')
plt.title('Top 5 Most Frequent Artists by Number of Tracks')
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()
```
#### Expected Results
<p align="center">
  <img src="https://github.com/user-attachments/assets/327e56bf-43c5-44d9-b4af-d7026e4d3cc7" alt="Centered Image">
</p>

# 🔴 Summary of Top Performers
🟣 The track with the highest number of streams in the dataset was found to be "Blinding Lights" by The Weeknd, with over 3.7 billion streams. This song leads the list of top-streamed tracks, followed closely by "Shape of You" by Ed Sheeran, which has over 3.5 billion streams. And when it comes to the most frequently appearing artists based on the number of tracks in the dataset, Taylor Swift tops the list with a remarkable 34 tracks, Followed by The Weeknd, who has 22 tracks. Bad Bunny and SZA each have 19 tracks, and Harry Styles rounds out the top five with 17 tracks. 

## Temporal Trends

- Get the value of number of songs released per year
```python
trackperyear = dataset['released_year'].value_counts().sort_index()
yearcounttable = trackperyear.reset_index()
```
- Rename the columns 
```python
yearcounttable.columns=['Released Year','Number of Songs']
```
- Print results
```python
print(yearcounttable.head())
print(yearcounttable.tail())
```
#### Expected Output
```
Released Year  Number of Songs
    0           1930                1
    1           1942                1
    2           1946                1
    3           1950                1
    4           1952                1
        Released Year  Number of Songs
    45           2019               36
    46           2020               37
    47           2021              119
    48           2022              402
    49           2023              175
```
### Plot for No.Tracks Released per Year

- Plotting the line plot for the count of songs per released year
```python
plt.figure(figsize=(12, 6))
sns.lineplot(x=trackperyear.index, y=trackperyear.values, marker="o", color='#957DAD')
plt.title("No.Tracks Released per Year")
plt.xlabel("Released Year")
plt.ylabel("Number of Tracks") # Rotate x-axis labels for better readability
plt.grid(True)
plt.show()
```
#### Expected Value
<p align="center">
  <img src="https://github.com/user-attachments/assets/c7fc70a5-1d00-459b-a2b7-3496e4205eb8" alt="Centered Image">
</p>


### Number of Tracks per Month

- To calculate the number of tracks per year, the command **<span style="background-color: #FFDFD3; color: black">'.value_counts'</span>** can be used
  - **Syntax** - varname = dataFrame['released_month'].valuecounts().sort_index()
  - **.value_counts()** - counts the occurrences of each unique value in the released_year column of dataset.
  - **.reset_index()** - used to properly format the table

- Get the number of Tracks released per month
```python
trackpermonth = dataset['released_month'].value_counts().reset_index()
```
- Sort values in ascending order
```python
trackpermonth = trackpermonth.sort_values(by='released_month')
trackmonthtable = trackpermonth.reset_index()
```
- Print the values
```python
print(trackmonthtable.head())
print(trackmonthtable.tail())
```

#### Expected Output

       index  released_month  count
    0      0               1    134
    1      9               2     61
    2      2               3     86
    3      7               4     66
    4      1               5    128
        index  released_month  count
    7      11               8     46
    8      10               9     56
    9       6              10     73
    10      4              11     80
    11      5              12     75

### Plot for No. Songs Released per Month

- Configure the figure size
```python
plt.figure(figsize=(20, 10))
```
- Create barplot
```python
sns.barplot(data=trackpermonth, x='released_month', y='count', palette='Accent',hue='released_month')
```
- Format the titles and labels
```python
plt.title("No. of Tracks Released per Month")
plt.xlabel("Released Month")
plt.ylabel("Number of Songs")
plt.show()
```
#### Expected Results
<p align="center">
  <img src="https://github.com/user-attachments/assets/361b3596-7796-4463-a883-5bbfd1b6dd44" alt="Centered Image">
</p>

# 🔴 Summary of Temporal Trends
:purple_circle: The analysis of track releases over time shows a clear upward trend, with a notable surge in recent years. Specifically, from 2021 to 2023, there was a significant increase in the number of tracks released. The peak occurred in 2022, with 402 songs released, followed by 2023 with 175. This rise likely reflects a growing trend in music production and more frequent releases in the age of the internet. Looking at monthly release patterns, January and May emerge as the months with the highest release counts, with January seeing around 134 songs and May slightly more. While there is some variation in releases across other months, these two months consistently have higher numbers, suggesting possible seasonal trends or intentional release strategies by artists and labels.

## Genre and Music Characteristics

### Correlation between streams and musical attributes

- In order to perform a correlational analysis **<span style="background-color: #FFDFD3; color: black">'.corr()'</span>** command
- **Syntax** - varname = dataframe['streams'].corr(dataframe.['musicalattribute'])

- Using the given syntax, get the correlation of streams between the three musical attributes
```python
bpmcor = dataset['streams'].corr(dataset['bpm'])
dancecor = dataset['streams'].corr(dataset['danceability_%'])
energycor = dataset['streams'].corr(dataset['energy_%'])
```
- Print the values of correlations
```python
print('Correlation Between Streams and BPM:',bpmcor)
print('\nCorrelation Between Streams and Danceability:', dancecor)
print('\nCorrelation Between Streams and Energy:', energycor)
```
#### Expected Output

 > Correlation Between Streams and BPM: -0.0020107392431484824
    
 > Correlation Between Streams and Danceability: -0.10445104424167974
    
 > Correlation Between Streams and Energy: -0.02631090790485633

 ### Plot for Correlations between streams

- Create a single figure with subplots for each scatter plot using plt.subplot
```python
plt.figure(figsize=(18, 6))
```
- Scatter plot for streams vs bpm in the first subplot
```python
plt.subplot(1, 3, 1)
sns.scatterplot(data=dataset, x='streams', y='bpm',color='#FD8A8A')
plt.title("Streams vs BPM")
plt.xlabel("Streams")
plt.ylabel("BPM")
```
- Scatter plot for streams vs danceability_% in the second subplot
```python
plt.subplot(1, 3, 2)
sns.scatterplot(data=dataset, x='streams', y='danceability_%',color='#9EA1D4')
plt.title("Streams vs Danceability_%")
plt.xlabel("Streams")
plt.ylabel("Danceability_%")
```
- Scatter plot for streams vs energy_% in the third subplot
```python
plt.subplot(1, 3, 3)
sns.scatterplot(data=dataset, x='streams', y='energy_%',color='#A8D1D1')
plt.title("Streams vs Energy_%")
plt.xlabel("Streams")
plt.ylabel("Energy_%")
```
- Adjust layout for clarity
```python
plt.tight_layout()
plt.show()
```
#### Expected Results
<p align="center">
  <img src="https://github.com/user-attachments/assets/66de4db0-160c-463c-a0da-8636d6593014" alt="Centered Image">
</p>


###  Correlations of Danceability vs Energy and Valence vs Acousticness
- Calculate the correlation between Danceability vs Energy
```python
dance_energy_corr = dataset['danceability_%'].corr(dataset['energy_%'])
```
- Calculate the correlation between Valence vs Acousticness
```python
val_acou_corr = dataset['valence_%'].corr(dataset['acousticness_%'])
```
- Print the correlation values
```python
print('Correlation Between Danceability and Energy:',dance_energy_corr)
print('\nCorrelation Between Valence and Acousticness:',val_acou_corr)
```
#### Expected Result

    Correlation Between Danceability and Energy: 0.1980948483762571
    
    Correlation Between Valence and Acousticness: -0.08190727483082756


### Plot for Correlations of Danceability vs Energy and Valence vs Acousticness

- Configure the figure size
```python
plt.figure(figsize=(18, 6))
```
- Create subplots to view both plots
- Scatter plot for streams vs bpm in the first subplot
```python
plt.subplot(1, 2, 1)
sns.scatterplot(data=dataset, x='danceability_%', y='energy_%',color='#957DAD')
plt.title("Danceability vs Energy")
plt.xlabel("Danceability")
plt.ylabel("Energy")
```
- Scatter plot for streams vs danceability_% in the second subplot
```python
plt.subplot(1, 2, 2)
sns.scatterplot(data=dataset, x='valence_%', y='acousticness_%',color='#D291BC')
plt.title("Valence vs Acousticness")
plt.xlabel("Valence")
plt.ylabel("Acousticness")
```
- Adjust layout for clarity
```python
plt.tight_layout()
plt.show()
```
#### Expected Result 
<p align="center">
  <img src="https://github.com/user-attachments/assets/ba481119-8285-4da9-9f7c-3ab75fa495b6" alt="Centered Image">
</p>

# Summary of Genre and Music Characteristics
🟣 The correlation analysis between streams and musical attributes, such as BPM, danceability, and energy reveals minimal influence of these factors on streaming popularity. Specifically, BPM has a correlation of approximately -0.002 with streams, indicating almost no relationship between a song’s tempo and its popularity. Danceability shows a slightly stronger correlation with streams at -0.104, though this relationship remains weak, suggesting that danceability does not significantly affect stream counts. Energy has a correlation of around -0.026 with streams, similarly showing negligible influence. Among these attributes, danceability has the highest correlation with streams, but it is still too weak to suggest a meaningful impact on a song’s popularity. 

🟣 Exploring correlations between other musical attributes, danceability and energy display a moderate positive correlation of 0.198, indicating that tracks with higher danceability tend to have higher energy. Additionally, valence and acousticness exhibit a stronger negative correlation of -0.819, suggesting that tracks with a happier sound (higher valence) are generally less acoustic. These correlations highlight some internal relationships between musical characteristics, but none of them have a substantial effect on streaming numbers.

## Platform Popularity

- To calculate total number of tracks per platforms' playlist/chart the command .sum() can be used
- **.sum()** - enables user to be able to get the total values of the column
- **Syntax** = varname = dataframe[platformtlist/chart].sum()

- Get the sum of the specified columns
```python
spotplaylist = dataset['in_spotify_playlists'].sum()
spotcharts = dataset['in_spotify_charts'].sum()
appleplaylist = dataset['in_apple_playlists'].sum()
```
- Print the values
```python
print('Number of Tracks in spotify_playlists:',spotplaylist)
print('\nNumber of Tracks in spotify_charts:', spotcharts)
print('\nNumber of Tracks in apple_playlists:',appleplaylist)
```
- Get the sum of the specified columns
```python
applecharts = dataset['in_apple_charts'].sum()
deezerlist = dataset['in_deezer_playlists'].sum()
deezercharts = dataset['in_deezer_charts'].sum()
```
- Total the data from charts and playlist for each platfotm
```python
appletotal = applecharts + appleplaylist
deezertotal = deezercharts + deezerlist 
spotifytotal = spotplaylist + spotcharts
shazamtotal= dataset['in_shazam_charts'].sum()
```
- Print results
```python
print('\n\nNumber of Tracks in Apple is:',appletotal)
print('\nNumber of Tracks in Deezer is:', deezertotal)
print('\nNumber of Tracks in Spotify is:', spotifytotal)
print('\nNumber of Tracks in Shazam is:', shazamtotal)
```
#### Expected Results

    Number of Tracks in spotify_playlists: 4955719
    
    Number of Tracks in spotify_charts: 11445
    
    Number of Tracks in apple_playlists: 64625
    
    
    Number of Tracks in Apple is: 114094
    
    Number of Tracks in Deezer is: 369625
    
    Number of Tracks in Spotify is: 4967164
    
    Number of Tracks in Shazam is: 54176


## Plotting the number of tracks in Spotify Playlist, Spotify Charts, and Apple Playlist

- Create a dictionary the contains Spotify Playlist, Spotify Charts, and Apple Playlist and its corresponding values 
```python
playlist_counts = {'Spotify Playlists': spotplaylist,'Spotify Charts': spotcharts,'Apple Playlists': appleplaylist}
```
- Configure the figure size
```python
plt.figure(figsize=(10, 6))
```
- Create a bar plot of the data
```python
sns.barplot(x=list(playlist_counts.keys()), y=list(playlist_counts.values()), palette='Blues',hue=list(playlist_counts.keys()))
```
- Format the labels and titles of the plot
```python
plt.xlabel('Playlist/Chart Type')
plt.ylabel('Number of Tracks')
plt.title('Number of Tracks in Spotify Playlists, Spotify Charts, and Apple Playlists')
plt.tight_layout()
plt.show()
```
#### Expected Result
<p align="center">
  <img src="https://github.com/user-attachments/assets/f6e6a2da-e108-4f62-a83c-83fb24d6161c" alt="Centered Image">
</p>


## Plotting number of tracks per platform

- Create a dictionary which contains the total number of tracks per platform
```python
platform_totals = {'Apple': appletotal, 'Deezer': deezertotal,'Spotify': spotifytotal, 'Shazam': shazamtotal}
```
- Configure figure size
```python
plt.figure(figsize=(10, 6))
```
- Create a barplot
```python
sns.barplot(x=list(platform_totals.keys()), y=list(platform_totals.values()), palette='coolwarm',hue=list(platform_totals.keys()))
```
- Put appropriate titles and labels
```python
plt.xlabel('Platform')
plt.ylabel('Total Tracks in Playlists/Charts')
plt.title('Platforms Favoring the Most Popular Tracks')
plt.tight_layout()
plt.show()
```
#### Expected Results
<p align="center">
  <img src="https://github.com/user-attachments/assets/14498e1b-1133-4ed1-896d-39c3bf6b5855" alt="Centered Image">
</p>

# 🔴 Summary of Platform Popularity
:purple_circle: The comparison between the number of tracks in spotify_playlists, spotify_charts, and apple_playlists shows notable differences in how these platforms curate and feature songs. The spotify_playlists category has the highest number of tracks, with approximately 4955719 tracks, indicating that Spotify playlists have a wide variety of songs available. Apple Playlists, with 64625 tracks, contain fewer entries, suggesting a more selective curation compared to Spotify’s playlists. Meanwhile, spotify_charts have only 11445 tracks, representing the most popular and trending songs on Spotify at any given time.

Given these numbers, it appears that Spotify playlists include a more extensive selection of music, whereas Spotify charts favor the most popular tracks due to their relatively smaller, curated list focused on current trends and hits. This suggests that Spotify may provide broader exposure for both mainstream and niche songs through its playlists, while Spotify charts specifically highlight the most popular tracks.

## Advanced Analysis

- create a dataset that contains'in_spotify_playlists', 'in_spotify_charts', 'in_apple_playlists', 'in_apple_charts', 'in_deezer_playlists', 'in_deezer_charts', 'in_shazam_charts'
```python
columns_track = ['in_spotify_playlists', 'in_spotify_charts', 'in_apple_playlists', 'in_apple_charts', 'in_deezer_playlists', 'in_deezer_charts', 'in_shazam_charts']
```
- Calculate the sum for each row across the specified columns and create a new column
```python
dataset['total_appearances'] = dataset[columns_track ].sum(axis=1)
```
- Group by key and mode and calculate the total track count, playlist/chart count, and streams
```python
spotify_summary = dataset.groupby(['key', 'mode']).agg(total_tracks=('track_name', 'size'),total_playlist_chart_count=('total_appearances', 'sum'),total_streams=('streams', 'sum')).reset_index()
```
- print results
```python
print(spotify_summary.head())
print('\n',spotify_summary.tail())
```
#### Expected Result

      key   mode  total_tracks  total_playlist_chart_count  total_streams
    0   0  Major            75                      378735   3.749617e+10
    1   0  Minor            20                      162928   1.201712e+10
    2   A  Major            42                      188364   1.648037e+10
    3   A  Minor            33                      112381   1.377389e+10
    4  A#  Major            27                      129337   1.694341e+10
    
        key   mode  total_tracks  total_playlist_chart_count  total_streams
    19  F#  Minor            43                      353276   2.560616e+10
    20   G  Major            66                      431685   3.253676e+10
    21   G  Minor            30                       98077   1.091278e+10
    22  G#  Major            63                      372811   3.438568e+10
    23  G#  Minor            28                       83303   9.013301e+09

### Plot for Total Tracks by Key and Mode

- Configure figuresize
```python
plt.figure(figsize=(10, 6))
```
- Create barplot of total tracks by Key and Mode
```python
sns.barplot(data=spotify_summary, x='key', y='total_tracks', hue='mode',palette='Purples')
```
- Configure the title and labels
```python
plt.title("Total Tracks by Key and Mode")
plt.xlabel("Key")
plt.ylabel("Total Tracks")
plt.legend(title="Mode")
plt.show()
```
#### Expected Result
<p align="center">
  <img src="https://github.com/user-attachments/assets/28282345-4797-4e80-b80b-e3e11ae73270" alt="Centered Image">
</p>


### Plot for Total Playlist/Chart Count by Key and Mode

- Sample plot showing total playlist/chart count by key and mode
```python
plt.figure(figsize=(10, 6))
```
- Create barplot of total playlist/chart count by Key and Mode
```python
sns.barplot(data=spotify_summary, x='key', y='total_playlist_chart_count', hue='mode',palette='Purples')
```
- Configure titles and lables
```python
plt.title("Total Playlist/Chart Count by Key and Mode")
plt.xlabel("Key")
plt.ylabel("Total Playlist/Chart Count")
plt.legend(title="Mode")
plt.show()
```
#### Expected Result
<p align="center">
  <img src="https://github.com/user-attachments/assets/1506d30d-6c35-45d9-b8aa-f2171a8f53d9" alt="Centered Image">
</p>


### Plot for Total Streams by Key and Mode

- Sample plot showing total streams by key and mode
```python
plt.figure(figsize=(10, 6))
```
- Create barplot of total streams by Key and Mode
```python
sns.barplot(data=spotify_summary, x='key', y='total_streams', hue='mode',palette='Purples')
```
- Configure titles and labels
```python
plt.title("Total Streams by Key and Mode")
plt.xlabel("Key")
plt.ylabel("Total Streams")
plt.legend(title="Mode")
plt.show()
```
#### Expected Result
<p align="center">
  <img src="https://github.com/user-attachments/assets/5c2de0a3-60bb-4689-aa7e-39ca07c15d65" alt="Centered Image">
</p>


# Top Artists per Total Appearances

- Calculate the total appearances across all platforms for each artist
- Create dataframe the contains the columns of playlist and charts of each platform
```python
totaldata = ['in_spotify_playlists', 'in_spotify_charts', 'in_apple_playlists','in_apple_charts', 'in_deezer_playlists', 'in_deezer_charts', 'in_shazam_charts']
```
- Calculate the total appearances in every platform
```python
dataset['total_appearances'] = dataset[totaldata].sum(axis=1)
dataset['total_appearances'].reset_index()
```
- Arrange the data from the top 10 highest total appearances
```python
top_artists_total_appearances = dataset.groupby('artist(s)_name')['total_appearances'].sum().nlargest(10).reset_index()
top_artists_total_appearances
```
#### Expected Result
<p align="center">
  <img src="https://github.com/user-attachments/assets/12b12aa8-5911-4e40-b874-4407e8d46e58" alt="Centered Image">
</p>


### Plot of Top Artist per Total Appearances

- Plotting the barplot for the top artists by total appearances
- Configure the figure size
```python
plt.figure(figsize=(14, 6))
```
- Create barplot of top artist per total appearances
```python
sns.barplot(y=top_artists_total_appearances['total_appearances'], x=top_artists_total_appearances['artist(s)_name'], palette="magma",hue=top_artists_total_appearances['artist(s)_name'])
```
- Configure titles and labels
```python
plt.title("Top 10 Artists by Playlist and Chart Appearances")
plt.xlabel("Artist Name")
plt.ylabel("Total Appearances")
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()
```
#### Expected Results
![image](https://github.com/user-attachments/assets/1d94d4ec-d240-4011-bc61-4e1539df2274)

# 🔴 Summary of Advanced Analysis 
:purple_circle: The analysis of streams data shows patterns based on musical key and mode. Tracks in keys like C# Major and G Major tend to have higher playlist and chart appearances, suggesting a preference for these keys in popular music. Additionally, major key tracks generally receive more streams than minor ones, indicating a slight favorability for major keys.

🟣 In terms of artist appearances, The Weeknd, Ed Sheeran, and Taylor Swift top the list, consistently appearing in playlists and charts. Other popular artists, such as Harry Styles and Eminem, also have a strong presence. This suggests that certain genres and artists are more widely promoted on music platforms, reflecting their broad appeal and influential role in current music trends.

# Thank you for reading! 💜🎊
