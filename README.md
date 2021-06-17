# Spotify Recommendation System
![cover_photo](./img/mixtapecover.jpg)

# Index
1.	[Introduction](#1-introduction)
2.	[Data Sources](#2-data-sources)
3.  [Data Wrangling](#3-data-wrangling)
4.  [EDA](#4-eda)
5.  [Modeling](#5-modeling)

## 1. Introduction
As a music lover, I spend most of my time in a day listening to music. I loved YouTube Music algorithm as it helps me discover a lot of new songs based on my preferred taste of music. I have never thought of implementing a music recommendation system on my own. However, after coincidentally exploring a kernel named [Music Recommendation System using Spotify Dataset](https://www.kaggle.com/vatsalmavani/music-recommendation-system-using-spotify-dataset) on Kaggle, I was inspired and decided to build a Spotify Recommendation System based on the algorithm already implemented in the kernel. However, I've modified the algorithm a bit when I was working on this project. I'll explain it deeply below. 

## 2. Data Sources
In this project, I learned how to scrape the data using the Spotify API. Here are the two resources: [[1]](https://towardsdatascience.com/become-a-lyrical-genius-4362e7710e43) and [[2]](https://github.com/christianlomboy/MIR-Genre-Predictor/blob/master/MIR_data_collection.ipynb) that helped me implement the notebook that allows me to scapre the data from any playlists on Spotify. Specifically, I defined a class called GetMeta() to get all metadata of a song from Spotify, including: `name`, `artists`, `popularity`, `genre`, `release date`, `popularity`, `danceability`, `energy`, `key`, `loudness`, `mode`, `speechiness`, `acousticness`, `instrumentalness`, `liveness`, `valence`, `tempo`, `duration_ms`, and `lyrics`. Therefore, I was able to scrape the data from multiple playlists in three different languages, including Mandarin, Korean, and Vietnamese, on Spotify. 

If you would like to scapre data from some of your favourite playlists on Spotify, all you need are: 
* genius_key
* spotify_client_id
* spotify_client_secret
* spotify_user_id
* spotify_playlist_id

There are three things that you need to do. 
1) Create an account with Genius [here](https://genius.com/signup_or_login). After you have an account, you should see an authorization code on the right hand side of the page. You may see there are multiple boxes say "Authorization: Bearer ........" Don't be tricked, they are all the same authorization code. You only need to copy the code from one of those boxes and paste into **genius_key**.   
2) Creating a developer account with Spotify if you have not had one. After logging into the dashboard, you will then need to create an application. Please give the application an exciting name and description and tick all of the boxes that apply for the “What are you building?” question. Once the application was live, please take note of both the Client ID and Client Secret, then paste them into **spotify_client_id** and **spotify_client_secret** respectively. 
3) Easy step! Go to your favorite playlist on Spotify -> click on three dots -> click on share -> click on copy link to playlist -> paste the link into **spotify_playlist_id**. Next, click on the name of the playlist's owner -> click on three dots -> click on copy link to profile -> paste the link into **spotify_user_id**. 

Woohoo! You are now able to scrape the data from any playlists on Spotify on your own!! 

## 3. Data Wrangling
As mentioned above, since we scraped the data from multiple playlists in different languages, we had a separate notebook for each language.
1) [Mandarin](https://github.com/tvo10/spotify-recommendation-system/blob/main/data_wrangling_by_language/spotify_recommendation_system_data_wrangling_mandopop.ipynb)
2) [Korean](https://github.com/tvo10/spotify-recommendation-system/blob/main/data_wrangling_by_language/spotify_recommendation_system_data_wrangling_kpop.ipynb)
3) [Vietnamese](https://github.com/tvo10/spotify-recommendation-system/blob/main/data_wrangling_by_language/spotify_recommendation_system_data_wrangling_vpop.ipynb)

In each notebook, there are 5 csv files that need to be merged to one dataset, including: 
* **names.csv:** The names of the songs 
* **artists.csv:** The artist(s) of the songs 
* **popularity.csv:** The popularity of the songs 
* **release_date.csv:** The release dates of the songs 
* **features.csv:** The features of the songs

As a result, we have three datasets, **mandopop.csv**, **kpop.csv**, and **vpop.csv**. Afterwards, we need to create a final dataset that combines all these three datasets together. Hence, our final dataset named **songs.csv**, which contains **6350 observations** and **17 variables**. 
Please see below for the final notebook where we merged all three datasets together and exported to a CSV file called **songs.csv**. 

[Data Wrangling](https://github.com/tvo10/spotify-recommendation-system/blob/main/02_spotify_recommendation_system_data_wrangling.ipynb)

## 4. EDA
There are two notebooks for EDA:
1) [EDA for All Songs](https://github.com/tvo10/spotify-recommendation-system/blob/main/03_01_spotify_recommendation_system_general_eda.ipynb): This notebook helps us obtain a general sense of our dataset. In other words, we explored all the observations and variables in this notebook.
2) [EDA for A Specific Language/Music](https://github.com/tvo10/spotify-recommendation-system/blob/main/03_02_spotify_recommendation_system_certain_music_eda.ipynb): This notebook is slightly different as it breaks the dataset down by language/music. For instance, we can understand the top 10 popular songs, top 10 famous artists, and top 10 artists with the most published songs in each language/music. Furthermore, we can compare all the features, such as tempo, valence, loudness, etc. of all three languages together. 
Please see below for some of the demonstrations in the **EDA for A Specific Language/Music** notebook.

<p>
    <img src="https://github.com/tvo10/spotify-recommendation-system/blob/main/img/mpop_10_songs.PNG" />
</p>
<hr style="width:40%">
<p>
  <img src="https://github.com/tvo10/spotify-recommendation-system/blob/main/img/mpop_10_artists.PNG" />
</p>
<hr style="width:40%">
<p>
  <img src="https://github.com/tvo10/spotify-recommendation-system/blob/main/img/mpop_10_artists_songs.PNG" />
</p>
<hr style="width:40%">
<p>
  <img src="https://github.com/tvo10/spotify-recommendation-system/blob/main/img/kpop_10_songs.PNG" />
</p>
<hr style="width:40%">
<p>
  <img src="https://github.com/tvo10/spotify-recommendation-system/blob/main/img/kpop_10_artists.PNG" />
</p>
<hr style="width:40%">
<p>
  <img src="https://github.com/tvo10/spotify-recommendation-system/blob/main/img/kpop_10_artists_songs.PNG" />
</p>
<hr style="width:40%">
<p>
  <img src="https://github.com/tvo10/spotify-recommendation-system/blob/main/img/vpop_10_songs.PNG" />
</p>
<hr style="width:40%">
<p>
  <img src="https://github.com/tvo10/spotify-recommendation-system/blob/main/img/vpop_10_artists.PNG" />
</p>
<hr style="width:40%">
<p>
  <img src="https://github.com/tvo10/spotify-recommendation-system/blob/main/img/vpop_10_artists_songs.PNG" />
</p>

For more details: 
[Exploratory Data Analysis](https://github.com/tvo10/spotify-recommendation-system/blob/main/03_02_spotify_recommendation_system_certain_music_eda.ipynb)


## 5. Modeling
As mentioned in the beginning, I've modified the algorithm from an extraordinary work on [Kaggle](https://www.kaggle.com/vatsalmavani/music-recommendation-system-using-spotify-dataset). Briefly, we have built a music recommendation system using the Spotify API and datasets. How does the system work? To simply put, we applied KMeans algorithm to cluster all the songs in three groups (k=3).
<p>
  <img src="https://github.com/tvo10/spotify-recommendation-system/blob/main/img/kmeans.PNG" />
</p>

We then used the Euclidean distance to measure the distance between each song based on the mean of the features, including `danceability`,`energy`, `key`, `loudness`, `mode`, `speechiness`, `acousticness`, `instrumentalness`, `liveness`, `valence`, `tempo`. We decide to use the Euclidean Distance over the Cosine Similarity since we believe that the magnitude matters as we want to listen to other songs with the features mean that is closest to our favourite song. For instance, if the mean of our favourite song's valence is 0.4, we do not want to listen to the song with the mean of valence is 0.7. Therefore the Euclidean Distance works best in our case.  
Our implemented function works like this:
<p>
  <img src="https://github.com/tvo10/spotify-recommendation-system/blob/main/img/demo.gif" />
</p>

For more details: 
[Modeling](https://github.com/tvo10/spotify-recommendation-system/blob/main/04_spotify_recommendation_system_modeling.ipynb)
