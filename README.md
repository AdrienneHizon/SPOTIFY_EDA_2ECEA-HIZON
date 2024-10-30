# 🎶 Exploratory Data Analysis on Spotify 2023 Dataset (Incentive) 🎵

## 📖 Introduction 
This project presents an exploratory data analysis (EDA) of the Most Streamed Spotify Songs 2023 dataset, focusing on trends, patterns, and insights in popular music streaming. Using Python and data visualization libraries, this analysis dives into the characteristics of top-streamed tracks, artist trends, and genre distributions to uncover key factors behind the year's biggest hits. This repository contains all code, visualizations, and insights to help understand the evolving dynamics in the music streaming landscape.
> [!NOTE]
> 💡 The analysis took place on the dataset that was posted in [Kaggle](https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023). You can download the dataset on the highlighted text for reference

## 🗂 Table of Contents
- [📖 Introduction](##📖-Introduction)
- [🗂 Table of Contents](##🗂-Table-of-Contents)
- [🖥 Overview of Dataset](##🖥-Overview-of-Dataset)

## 🖥 Overview of Dataset

> [!IMPORTANT]
> ❗ Importing these libraries is essential for data analysis and visualizations

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from math import *
```
The downloaded csv file from data analysis is stored inside the spotify variable with an encoding of latin-1

```python
spotify = pd.read_csv('spotify-2023.csv', encoding='latin-1')
spotify
```
![image](https://github.com/user-attachments/assets/10943318-a12c-4cba-ade5-7bc322d51c8d)

The dataframe above contains the top 953 songs from spotify with 24 columns of different information that can range in presence of other apps such as Apple Music and Deezers, general informations and charts, and musical characteristics
