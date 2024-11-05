# 🎶 Exploratory Data Analysis on Spotify 2023 Dataset (Incentive) 🎵

## 📖 Introduction 
This project presents an exploratory data analysis (EDA) of the Most Streamed Spotify Songs 2023 dataset, focusing on trends, patterns, and insights in popular music streaming. Using Python and data visualization libraries, this analysis dives into the characteristics of top-streamed tracks, artist trends, and genre distributions to uncover key factors behind the year's biggest hits. This repository contains all code, visualizations, and insights to help understand the evolving dynamics in the music streaming landscape.
> [!NOTE]
> 💡 The analysis took place on the dataset that was posted in [Kaggle](https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023). You can download the dataset on the highlighted text for reference

## 🗂 Table of Contents
- 📖 Introduction
- 🗂 Table of Contents
- 🖥 Overview of Dataset
- 📡 General Informations
  - 📂 Null Count and Datatype
- 📈 Statistics, Outliers, Trends, etc.
  - 📏 General Statistics
  - 〽️ STREAM STATISTICS: Mean, Median, and Standard Deviation
  - 📅 Released Year and Artist Count Distribution Statistics
- Hello


## 🖥 Overview of Dataset

> [!IMPORTANT]
> ❗ Importing these libraries is essential for data analysis and visualizations

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from math import *
```
The downloaded csv file from data analysis is stored inside the spotify variable with an encoding of latin-1

```python
spotify = pd.read_csv('spotify-2023.csv', encoding='latin-1')
spotify
```
![image](https://github.com/user-attachments/assets/10943318-a12c-4cba-ade5-7bc322d51c8d)

The dataframe above contains the top 953 songs from spotify with 24 columns of different information that can range in presence of other apps such as Apple Music and Deezers, general informations and charts, and musical characteristics

## 📡 General Informations

The Row and Columns display is shown for general information purposes

```python
print(f"Rows: {spotify.shape[0]} \nColumns: {spotify.shape[1]}")
```

Output:
```python
Rows: 953 
Columns: 24
```


### 📂 Null Count and Datatype
This section will display the number of non-null counts and its datatype details.

```python
spotify.info()
```

Output:

```python
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 953 entries, 0 to 952
Data columns (total 24 columns):
 #   Column                Non-Null Count  Dtype 
---  ------                --------------  ----- 
 0   track_name            953 non-null    object
 1   artist(s)_name        953 non-null    object
 2   artist_count          953 non-null    int64 
 3   released_year         953 non-null    int64 
 4   released_month        953 non-null    int64 
 5   released_day          953 non-null    int64 
 6   in_spotify_playlists  953 non-null    int64 
 7   in_spotify_charts     953 non-null    int64 
 8   streams               953 non-null    object
 9   in_apple_playlists    953 non-null    int64 
 10  in_apple_charts       953 non-null    int64 
 11  in_deezer_playlists   953 non-null    object
 12  in_deezer_charts      953 non-null    int64 
 13  in_shazam_charts      903 non-null    object
 14  bpm                   953 non-null    int64 
 15  key                   858 non-null    object
 16  mode                  953 non-null    object
 17  danceability_%        953 non-null    int64 
 18  valence_%             953 non-null    int64 
 19  energy_%              953 non-null    int64 
 20  acousticness_%        953 non-null    int64 
 21  instrumentalness_%    953 non-null    int64 
 22  liveness_%            953 non-null    int64 
 23  speechiness_%         953 non-null    int64 
dtypes: int64(17), object(7)
memory usage: 178.8+ KB
```

A more detailed of null counts will be displayed in this line of code

```python
spotify.isnull().sum()
```

Output:

```python
track_name               0
artist(s)_name           0
artist_count             0
released_year            0
released_month           0
released_day             0
in_spotify_playlists     0
in_spotify_charts        0
streams                  0
in_apple_playlists       0
in_apple_charts          0
in_deezer_playlists      0
in_deezer_charts         0
in_shazam_charts        50
bpm                      0
key                     95
mode                     0
danceability_%           0
valence_%                0
energy_%                 0
acousticness_%           0
instrumentalness_%       0
liveness_%               0
speechiness_%            0
dtype: int64
```
Key and in_deezer_charts have the most amount of null values

## 📈 Statistics, Outliers, Trends, etc.

### 📏 General Statistics
This will display the general statistics of the table (streams not included, as it is analyzed in the other section)

```python
spotify.describe()
```

![image](https://github.com/user-attachments/assets/8fdba8f0-ae2a-4fcd-9a23-a150490abff7)


![image](https://github.com/user-attachments/assets/3255a324-6872-42a8-bf31-237f62193a55)


### 〽️ STREAM STATISTICS: Mean, Median, and Standard Deviation

```python
# Calculate for the statistics
mean = round(np.mean(spotify['streams']),2)
median = spotify['streams'].dropna().median()
std = round(np.std(spotify['streams']),2)

print(f"STREAM STATISTICS:\n\nMean: {mean}\nMedian: {median}\nStandard Deviation: {std}")
```

Output:
```python
STREAM STATISTICS:

Mean: 514137424.94
Median: 290530915.0
Standard Deviation: 566559151.83
```

### 📅 Released Year and Artist Count Distribution Statistics

This will count the occurrences of each release year and artists count

```python
year_counts = spotify['released_year'].value_counts().sort_index()
artist_count_distribution = spotify['artist_count'].value_counts().sort_index()
```

Plotting the distribution of tracks by released year

```python
plt.figure(figsize=(10, 5))
year_counts.plot(kind='bar')
plt.title('Distribution of Tracks by Released Year')
plt.xlabel('Year')
plt.ylabel('Number of Tracks')
plt.show()
```

![image](https://github.com/user-attachments/assets/77014e2e-9c96-4424-9c1b-3221e806840c)

Observed on the data above, there was a large spike of released tracks in year 2022. This shows that the year 2022 has the greatest amount of notable music that were released in that year. At the start of 2014, the popular musics and trends starts to rise

Plotting the distribution tracks by artist count (will use seaborn styles)

```python
sns.set(style="darkgrid", palette="muted", font_scale=1.1)

plt.figure(figsize=(10, 6))
sns.histplot(data=spotify, x='artist_count', binwidth=1, color="lightcoral", edgecolor="black")
plt.title("Distribution of Tracks by Artist Count", fontsize=16, fontweight='bold', color='darkred')
plt.xlabel("Number of Artists", fontsize=14, color='gray')
plt.ylabel("Number of Tracks", fontsize=14, color='gray')
plt.xticks(color='gray')
plt.yticks(color='gray')
plt.show()
```

![image](https://github.com/user-attachments/assets/9d99a04c-569d-4223-bf33-e114f55d4348)

Observed on the data above, the distribution of tracks by artist count was found out that most tracks that were released were made solo. Though, there are still great numbers of tracks that were released with a collaboration with other artists.
























