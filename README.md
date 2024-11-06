# 🎶 Exploratory Data Analysis on Spotify 2023 Dataset (Incentive) 🎵

![image](https://github.com/user-attachments/assets/f70e229d-46af-4738-81ec-1c4a3ca1ac15)




## 📖 Introduction 
This project presents an exploratory data analysis (EDA) of the Most Streamed Spotify Songs 2023 dataset, focusing on trends, patterns, and insights in popular music streaming. Using Python and data visualization libraries, this analysis dives into the characteristics of top-streamed tracks, artist trends, and genre distributions to uncover key factors behind the year's biggest hits. This repository contains all code, visualizations, and insights to help understand the evolving dynamics in the music streaming landscape.
> [!NOTE]
> 💡 The analysis took place on the dataset that was posted in [Kaggle](https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023). You can download the dataset on the highlighted text for reference

## 🗂 Table of Contents
- [📖 Introduction](#-introduction)
- [🗂 Table of Contents](#-table-of-contents)
- [🖥 Overview of Dataset](#-overview-of-dataset)
- [📡 General Informations](#-general-informations)
  - [📂 Null Count and Datatype](#-null-count-and-datatype)
- [📈 Statistics, Outliers, Trends, etc.](#-statistics-outliers-trends-etc)
  - [📏 General Statistics](#-general-statistics)
  - [〽️ STREAM STATISTICS: Mean, Median, and Standard Deviation](#%EF%B8%8F-stream-statistics-mean-median-and-standard-deviation)
  - [📅 Released Year and Artist Count Distribution Statistics](#-released-year-and-artist-count-distribution-statistics)
- [🏆 Top Performers in Spotify](#-top-performers-in-spotify)
  - [🏅 Top 5 Songs in Spotify (2023)](#-top-5-songs-in-spotify-2023)
  - [⭐ Top 5 Most Frequent Artist](#-top-5-most-frequent-artist)
- [🎺 Temporal Trends](#-temporal-trends)
  - [📰 Yearly Trends](#-yearly-trends)
  - [🕓 Monthly Trends](#-monthly-trends)
- [🎸 Genre and Music Characteristics](#-genre-and-music-characteristics)
  - [🔀 Streams and Attributes Correlation](#-streams-and-attributes-correlation)
  - [⚛ Attributes Correlation](#-attributes-correlation)
- [📻 Platform Popularity, Patterns, and Consistency](#-platform-popularity-patterns-and-consistency)
  - [💾 Platform Comparison](#-platform-comparison)
  - [🎹 Keys Distribution](#-keys-distribution)
  - [📣 Top 10 Most Frequent Artists on Charts](#-top-10-most-frequent-artists-on-charts)
- [🗒 Conclusion](#-conclusion)
- [🔑 Author](#-author)

## 🖥 Overview of Dataset

This section provides an overview of the dataset used for analyzing the most streamed songs on Spotify in 2023, detailing its key components, such as track attributes, streaming counts, and artist information, which serve as the foundation for our analysis.

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

Here, we summarize general information from the dataset, including distributions by artist, genre, and release year, to establish context and identify potential patterns in music streaming behaviors.


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

In this section, we present statistical insights, focusing on metrics like mean and median streaming counts, while identifying outliers and trends to uncover significant patterns in listener behavior and streaming performance.

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

## 🏆 Top Performers in Spotify

We highlight the top-performing songs and artists based on streaming figures, exploring the factors contributing to their success and providing a snapshot of the competitive landscape within Spotify's music ecosystem.

### 🏅 Top 5 Songs in Spotify (2023)

To display the top performers in spotify, ensure that there's no null values that will hinder its computation. Therefore:

```python
spotify['streams'] = pd.to_numeric(spotify['streams'].astype(str).str.replace(',', ''), errors='coerce')
top_5_streams_df = spotify.sort_values(by='streams', ascending=False).head(5).reset_index(drop=True)
top_5_streams_df
```

![image](https://github.com/user-attachments/assets/5e5a36d1-6303-4433-8822-6a2124a0b2c8)

On the table, Blinding lights by the Weeknd has 3 billion streams on spotify and is at spotify charts 69 times

### ⭐ Top 5 Most Frequent Artist

```python
top_artists = spotify['artist(s)_name'].str.split(', ').explode().value_counts().head(5)
top_artists_df = top_artists.reset_index()
top_artists_df.columns = ['Artist', 'Track Count']

top_artists_df
```
![image](https://github.com/user-attachments/assets/bbe03c9f-2c8a-4c33-ab69-e0ab37d1e123)

Leading artist was Bad Bunny having 40 tracks in the spotify popular lists, second leading is Taylor Swift with 38 tracks in the spotify popular list

## 🎺 Temporal Trends

This section examines temporal trends in music streaming, analyzing how song popularity varies over time. We will also consider attributes such as danceability, valence, energy, BPM, and acousticness to understand how these characteristics influence listener engagement and streaming figures throughout different periods.

### 📰 Yearly Trends

Plot the number of tracks by release year with seaborn styling

```python
# Number of tracks by release year
tracks_per_year = spotify['released_year'].value_counts().sort_index()

# Plotting the trend over time
plt.figure(figsize=(12, 6))
tracks_per_year.plot(kind='bar', color='teal')
plt.xlabel('Year')
plt.ylabel('Number of Tracks')
plt.title('Distribution of Tracks by Released Year')
plt.show()
```
![image](https://github.com/user-attachments/assets/9a9ac8cf-892c-4ff5-aaed-9ea1316a5677)

Theres a significant trend of popular music that arisen back in year 2022

Grouping the musical characteristics and plotting it in a line graph for correlations

```python
# Group by released_year and calculate the average of each musical attribute
attributes_by_year = spotify.groupby('released_year')[['danceability_%', 'energy_%', 'acousticness_%', 'valence_%']].mean()

# Plotting trends for each attribute
plt.figure(figsize=(12, 6))
for attribute in attributes_by_year.columns:
    plt.plot(attributes_by_year.index, attributes_by_year[attribute], label=attribute)

plt.xlabel('Year')
plt.ylabel('Average Value')
plt.title('Yearly Average of Musical Attributes')
plt.legend()
plt.show()
```

![image](https://github.com/user-attachments/assets/eddde384-a137-4db2-ba35-aad20d0cd2b3)

As year goes by, there 4 musical attributes are fighting for trends, as of 21th century, the leading characteristics are danceability and energy

### 🕓 Monthly Trends

Counting values in the released_month and plotting it inside the bar graph

```python
# Count the number of tracks by release month
tracks_per_month = spotify['released_month'].value_counts().sort_index()

# Plotting the trend by month
plt.figure(figsize=(10, 5))
tracks_per_month.plot(kind='bar', color='skyblue')
plt.xlabel('Month')
plt.ylabel('Number of Tracks')
plt.title('Distribution of Tracks by Release Month')
plt.xticks(ticks=range(12), labels=['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'])
plt.show()
```

![image](https://github.com/user-attachments/assets/015ed737-5ea9-4c64-8671-c086c59e5747)

Based on the observed pattern, there has been a boom of popular music when its the month of January and May

Grouping attributes by months released and plotting it in a line graph

```python
# Group by released_month and calculate the average of each musical attribute
attributes_by_month = spotify.groupby('released_month')[['danceability_%', 'energy_%', 'acousticness_%', 'valence_%']].mean()

# Plotting trends for each attribute
plt.figure(figsize=(10, 5))
for attribute in attributes_by_month.columns:
    plt.plot(attributes_by_month.index, attributes_by_month[attribute], label=attribute)

plt.xlabel('Month')
plt.ylabel('Average Value')
plt.title('Monthly Average of Musical Attributes')
plt.legend()
plt.xticks(ticks=range(1, 13), labels=['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'])
plt.show()
```

![image](https://github.com/user-attachments/assets/6b73bb48-c0e2-405f-ba7b-04e40ca339f5)

Based on the observed graph, there has been a consistent leading of danceability and energy as an attribute as months go by


## 🎸 Genre and Music Characteristics

In this section, we analyze the relationship between music genres and their characteristics, focusing on attributes like danceability, valence, energy, BPM, and acousticness. By exploring how these features vary across genres, we aim to uncover trends and preferences that shape streaming success and influence listener choices on Spotify.

### 🔀 Streams and Attributes Correlation

Convert columns to numeric to avoid NaN errors

```python
# Convert columns to numeric, coercing errors to NaN
columns_to_convert = ['streams', 'bpm', 'danceability_%', 'energy_%', 'valence_%', 'acousticness_%']
for col in columns_to_convert:
    spotify[col] = pd.to_numeric(spotify[col], errors='coerce')

# Calculate the correlation matrix
corr_matrix = spotify[['streams', 'bpm', 'danceability_%', 'energy_%', 'valence_%', 'acousticness_%']].corr()

# Set a dark style for the heatmap
sns.set(style="dark", font_scale=1.2)

plt.figure(figsize=(10, 8))
sns.heatmap(corr_matrix, annot=True, fmt=".2f", cmap="coolwarm", linewidths=0.5, linecolor="black",
            annot_kws={"size": 12, "color": "black"}, cbar_kws={"shrink": 0.8})
plt.title("Correlation Heatmap of Musical Attributes and Streams", fontsize=16, fontweight='bold', color='lightblue')
plt.xticks(rotation=45, ha='right', color='gray')
plt.yticks(rotation=0, color='gray')
plt.show()
```

![image](https://github.com/user-attachments/assets/ed151aa5-cad3-454b-889f-b8f346855d4d)

In the heatmap that was constructed almost every attributes has negative correlation when its related to streams, meaning, characteristics has nothing to do with popularity because of the difference of preferences by other people

Plotting the correlations of streams and musical attributes to a scatterplot graph using seaborn

```python
# Scatter plots with Streams and additional attribute Valence
fig, axes = plt.subplots(1, 4, figsize=(24, 5))

# Streams vs Danceability
sns.scatterplot(ax=axes[0], x='danceability_%', y='streams', data=spotify)
axes[0].set_title("Streams vs Danceability %")

# Streams vs BPM
sns.scatterplot(ax=axes[1], x='bpm', y='streams', data=spotify)
axes[1].set_title("Streams vs BPM")

# Streams vs Energy
sns.scatterplot(ax=axes[2], x='energy_%', y='streams', data=spotify)
axes[2].set_title("Streams vs Energy %")

# Streams vs Valence
sns.scatterplot(ax=axes[3], x='valence_%', y='streams', data=spotify)
axes[3].set_title("Streams vs Valence %")

plt.tight_layout()
plt.show()
```

![image](https://github.com/user-attachments/assets/eeff98f6-243e-41e7-9196-fe1ca2144546)


On the scatterplot that was constructed, there's no significant correlation of how different attributes should be to boost the count of streams on music, it is not correlated on how a music is going to be popular. This discovery has made a realization that it does not matter what characteristics in music a piece of good music should be

### ⚛ Attributes Correlation

Plotting attributes in the scatterplot graph with seaborn styling

```python
fig, axes = plt.subplots(1, 2, figsize=(12, 5))

# Danceability vs Energy
sns.scatterplot(ax=axes[0], x='danceability_%', y='energy_%', data=spotify)
axes[0].set_title("Danceability % vs Energy %")

# Valence vs Acousticness
sns.scatterplot(ax=axes[1], x='valence_%', y='acousticness_%', data=spotify)
axes[1].set_title("Valence % vs Acousticness %")

plt.tight_layout()
plt.show()
```

![image](https://github.com/user-attachments/assets/412d41b4-b1ee-443b-a3f8-1a12491ea2df)

There has been a good correlation when the comparison of danceability and energy takes place. Valence and acousticness almost has no correlation with each other as they are independent. An increase of danceability factor also increases the energy level of a music and vice versa


## 📻 Platform Popularity, Patterns, and Consistency

This section explores the popularity and performance of Spotify, Apple Music, and Deezer, analyzing user engagement patterns and consistency in streaming behaviors across these platforms. We will highlight key notes, such as major and minor trends, as well as frequently streamed artists, to uncover how these platforms differ in their appeal and user preferences within the music streaming landscape.

### 💾 Platform Comparison

Ensure that there will be no NaN errors by converting columns to numeric; plotting a successful data on a bar graph

```python
# Attempt to convert columns to numeric, setting errors='coerce' to convert non-numeric values to NaN
columns_to_convert = ['in_spotify_playlists', 'in_spotify_charts', 'in_apple_playlists', 'in_deezer_playlists', 'in_deezer_charts']
spotify[columns_to_convert] = spotify[columns_to_convert].apply(pd.to_numeric, errors='coerce')

# Sum of tracks on different platforms
platform_data = spotify[columns_to_convert].sum().reset_index()
platform_data.columns = ['Platform', 'Count']

# Plotting
plt.figure(figsize=(12, 6))
sns.barplot(data=platform_data, x='Platform', y='Count', hue='Platform', dodge=False, palette='viridis')
plt.title('Number of Tracks by Platform', fontsize=16, fontweight='bold')
plt.xlabel('Platform', fontsize=14)
plt.ylabel('Number of Tracks', fontsize=14)
plt.xticks(rotation=45)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.show()
```

![image](https://github.com/user-attachments/assets/18ca7030-ec29-4992-80ea-8c7712ad2cf5)


Based on the bar graph that was shown, Spotify playlists have the most popular songs stored among all platforms

### 🎹 Keys Distribution

Counting the key distribution on tracks and plotting its frequency on a graph

```python
# Count of tracks by key and mode
key_mode_counts = spotify.groupby(['key', 'mode']).size().reset_index(name='Count')

# Plotting
plt.figure(figsize=(12, 8))
sns.barplot(data=key_mode_counts, x='key', y='Count', hue='mode', palette='coolwarm', dodge=False)
plt.title('Distribution of Tracks by Key and Mode', fontsize=16, fontweight='bold')
plt.xlabel('Key', fontsize=14)
plt.ylabel('Number of Tracks', fontsize=14)
plt.xticks(rotation=45)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.legend(title='Mode', title_fontsize='13', fontsize='11', loc='upper right')
plt.show()
```

![image](https://github.com/user-attachments/assets/6c1ec21d-39dd-42e5-b599-1db57ab6a268)

On the Bar Graph that was plotted, the C# has the most presence in the number of tracks for being either a Minor or Major; while D# is being the least used Minor and A being the least used Major

### 📣 Top 10 Most Frequent Artists on Charts

Plotting the most frequent artist on charts

```python
# Count the occurrences of each artist across all relevant columns
platform_columns = ['in_spotify_playlists', 'in_spotify_charts', 'in_apple_playlists', 'in_apple_charts', 'in_deezer_playlists', 'in_deezer_charts']
artist_counts = spotify.groupby("artist(s)_name")[platform_columns].sum().sum(axis=1).sort_values(ascending=False)

# Select the top 10 most frequently appearing artists in playlists and charts
top_artists = artist_counts.head(10).reset_index()
top_artists.columns = ['Artist', 'Appearances']

# Plotting
plt.figure(figsize=(14, 7))
sns.barplot(data=top_artists, x='Appearances', y='Artist', hue='Artist', dodge=False, palette="coolwarm", legend=False)
plt.title('Top 10 Most Frequently Appearing Artists in Playlists/Charts', fontsize=16, fontweight='bold')
plt.xlabel('Appearances in Playlists/Charts', fontsize=14)
plt.ylabel('Artist', fontsize=14)
plt.grid(axis='x', linestyle='--', alpha=0.7)
plt.show()
```

![image](https://github.com/user-attachments/assets/33895694-ba28-4395-b564-b17ac4aeef6d)

The Top 3 Artists frequently appearing in playlist and charts are The Weeknd, Taylor Swift, and Ed Sheeran. They are known for their Pop, Romance, and RnB songs

## 🗒 Conclusion

In this analysis, we have explored the dynamics of music streaming in 2023 through a comprehensive examination of the most streamed songs on Spotify, Apple Music, and Deezer. By delving into the dataset's overview and general information, we established a foundational understanding of the key characteristics and trends in the music landscape. Our statistical analysis highlighted significant patterns and outliers that reflect listener behavior, while the exploration of top performers showcased the factors contributing to success in the streaming realm. Additionally, we identified temporal trends and analyzed genre-specific characteristics to gain insights into how different attributes influence streaming popularity. Finally, our examination of platform popularity revealed distinct user engagement patterns across Spotify, Apple Music, and Deezer, emphasizing the competitive nature of the music streaming industry. Overall, this analysis provides valuable insights into the evolving preferences of music listeners and the factors that shape the success of tracks and artists across platforms.

## 🔑 Author
- Name: Kyle Adrienne S. Hizon
- Section: 2ECE-A


























