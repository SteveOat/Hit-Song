<hr>

<h1 align=center>CREATING BILLBOARD'S HIT SONG</h1>

![image](https://github.com/user-attachments/assets/bc283f6a-0031-41d0-99fc-2e7ebb8afe97)

[Billboard 2024](https://www.youtube.com/shorts/eFMNFWMn13E)

<hr>

<h1>Introducing Dataset</h1>

| df_1 Index | Column Name| Data Type |---| df_2 Index  | Column  | Data Type   |
|---|---|---|---|---|---|---|    
|0|Track|object|---| 0  | Unnamed: 0       | int64   |
|1|Artist|object|---| 1  | Artist and Title | object  |
| 2| Album | object |---|  2  | Artist           | object  |
| 3 | Year | int64   |---| 3  | Streams          | int64   |
| 4| Duration  | int64   |---| 4  | Daily            | int64   |
| 5 | Time_Signature  | int64  |---| 5  | year             | float64 |
| 6 | Danceability | float64   |---| 6  | main_genre       | object  |
| 7 | Energy  | float64  |---| 7  | genres           | object  |
| 8  | Key | int64   |---| 8  | first_genre      | object  |
| 9 | Loudness | float64 |---|  9  | second_genre     | object  |
| 10 | Mode | int64  |---| 10 | third_genre      | object  |
| 11 | Speechiness    | float64   |---| 
| 12  | Acousticness  | float64   |---| 
| 13 | Instrumentalness   | float64   |---| 
| 14| Liveness  | float64   |---| 
| 15| Valence| float64   |---| 
| 16 | Tempo| float64   |---| 
| 17| Popularity|int64     |---| 

<h3>Hit100.csv</h3>

> df_1

&nbsp;&nbsp;&nbsp;&nbsp; The dataset offers a detailed overview of contemporary music, featuring 620 tracks from 87 chart-topping artists between 2000 and 2023. It highlights the diversity of modern pop and R&B, capturing the evolution of Hot 100 hits over two decades. Each track is annotated with Spotify's audio features, providing insights into characteristics like tempo, energy, danceability, and valence, making it a valuable resource for exploring trends in popular music.

<h3>spotify_full_list_20102023.csv</h3>

> df_2

&nbsp;&nbsp;&nbsp;&nbsp;This dataset provides a look at the most streamed songs on Spotify from 2010 to 2023. Sourced from the Kworb Spotify toplists and enriched with genre data from the Spotify API, this dataset provides a glance at the music trends evolution over 14 years.

<h1>Key finding</h1>

Working on Spotify's api data
1. Visualize characteristics of hit songs on Billboard charts.
2. Find the most streamed genre on platform.
3. Does the artist's fame affect whether a song makes it onto the Billboard charts?

<h1 align=center>What is "Billboard" and Why "Spotify"</h1>
Songs make it to the **Billboard** charts (Top Hot 100) based on three key factors:

1. *Streaming* : Plays on platforms like ***Spotify***, Apple Music, YouTube, etc.
2. *Sales* : Digital and physical sales (e.g., iTunes, vinyl).
3. *Radio Airplay* : Number of times the song is played on radio stations.

Billboard compiles this data weekly from sources like Nielsen SoundScan and MRC Data to rank songs.<br>The combination of these factors determines a song's position on the charts.

![image](https://github.com/user-attachments/assets/a24b16ae-3ca9-487a-8ff6-6542de7209f4)

<hr>

<h1>Preparing Data</h1>

> Remove **Bracket "()"**  from "Track" column to match the text format of song's name.

> Remove **Space " "** and transform every text to lowercase.

> Splits **"Artist and Title"** into **"Artist"** , **"Track"**

> Merge the tables and filled *NaN* value in **"main_genre"** with *Unknown*.

> Remove duplicate **"Artist"** column that happened after merging.

> Create new column by combining rows that have the same song name but are sung by different artists to differentiate them.

|index|Track|Artist|Album|Year|Duration|Time\_Signature|Danceability|Energy|Key|Loudness|Mode|Speechiness|Acousticness|Instrumentalness|Liveness|Valence|Tempo|Popularity|Artist\_No\_Space|main\_genre|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|0|7rings|Ariana Grande|thank u, next|2019|178626|4|0\.78|0\.321|1|-10\.747|0|0\.372|0\.562|0\.0|0\.0881|0\.315|139\.961|50|arianagrande|Pop|
|1|breakfree|Ariana Grande|My Everything - Deluxe|2014|214840|4|0\.686|0\.702|7|-5\.325|0|0\.0455|0\.00637|4\.46e-05|0\.204|0\.29|129\.948|76|arianagrande|Pop|
|2|dangerouswoman|Ariana Grande|Dangerous Woman|2016|235946|3|0\.664|0\.602|4|-5\.369|0|0\.0412|0\.0529|0\.0|0\.356|0\.289|134\.049|70|arianagrande|Pop|
|3|godisawoman|Ariana Grande|Sweetener|2018|197546|4|0\.602|0\.658|1|-5\.934|1|0\.0558|0\.0233|6e-05|0\.237|0\.268|145\.031|75|arianagrande|Pop|
|4|intoyou|Ariana Grande|Dangerous Woman|2016|244453|4|0\.623|0\.734|9|-5\.948|1|0\.107|0\.0162|1\.75e-06|0\.145|0\.37|107\.853|71|arianagrande|Pop|

<hr>

<h2>1. Visualize characteristics of hit songs on Billboard charts.</h2>

<h3>1. Key Signature</h3>

&nbsp;&nbsp;&nbsp;&nbsp;**Cluster the Key signature**


|Cluster\_Key|Key|
|---|---|
|C|0|
|C\#/Db|1|
|D|2|
|Eb|3|
|E|4|
|F|5|
|F\#/Gb|6|
|G|7|
|G\#/Ab|8|
|A|9|
|A\#/Bb|10|
|B|11|
*   Musical key of the track, represented by integers (0 = C, 1 = C#/Db, etc.).

<h3>Plot the graph</h3>

![newplot](https://github.com/user-attachments/assets/0a3515db-6d85-4f76-bde0-336cb21d78c7)

&nbsp;&nbsp;&nbsp;&nbsp;**B , C and C#/Db :**

> The keys B, C, and C#/Db dominate this dataset, while Eb and A#/Bb are the least represented. It seems the dataset leans heavily on certain keys while others are used less frequently.

<h3>2. Mode</h3>

&nbsp;&nbsp;&nbsp;&nbsp;**Cluster the Mode**

|Cluster\_Mode|Mode|
|---|---|
|Minor|0|
|Major|1|
* Indicates whether the track is in a major (1) or minor (0) key.

<h3>Plot the graph</h3>

![newplot (2)](https://github.com/user-attachments/assets/b48fb2e5-7ed3-47a2-87b7-9827cabdfc9d)

&nbsp;&nbsp;&nbsp;&nbsp;Major Mode:
> Most songs in the dataset are in a major key, making up almost two-thirds of the total. A smaller chunk, just over a third, are in a minor key, which tends to give songs a different, more emotional vibe.

<h3>3. Duration</h3>

&nbsp;&nbsp;&nbsp;&nbsp;**Cluster the Duration**

|Cluster\_Duration\(Min\)|Duration|
|---|---|
|0-3mins|0 - 180,000 ms|
|3-5mins|180,001 - 300,000 ms|
|5+mins|300,001 ms and above |
- Length of the track, usually in milliseconds.
 - Short: 0 - 180,000 ms (0 - 3 minutes)
 - Medium: 180,001 - 300,000 ms (3 - 5 minutes)
 - Long: 300,001 ms and above (5+ minutes)

<h3>Plot the graph</h3>

![newplot (4)](https://github.com/user-attachments/assets/c9060aa4-32c9-47ee-a799-8df729eeb141)

&nbsp;&nbsp;&nbsp;&nbsp;3-5 minutes song :

> Tracks between 3-5 minutes dominate. The majority of the tracks, 462 in total, fall within the 3-5 minute range. This indicates that most tracks in the dataset are of moderate length, which is a common duration for popular music.

<h3>4. Danceability</h3>

&nbsp;&nbsp;&nbsp;&nbsp;**Cluster the Danceability**

|Cluster\_Danceability|Danceability|
|---|---|
|High\_Dance| 0.7 - 1.0|
|Mid\_Dance|0.4 - 0.7|
|Low\_Dance| 0.0 - 0.4|
- How suitable a track is for dancing, from 0.0 to 1.0.
 - Low: 0.0 - 0.4 (e.g., classical, ambient)
 - Medium: 0.4 - 0.7 (e.g., soft rock, indie)
 - High: 0.7 - 1.0 (e.g., pop, dance, hip-hop)

<h3>Plot the graph</h3>

![newplot (6)](https://github.com/user-attachments/assets/bc7b53c0-cfbc-423d-866c-146ce89d5681)

&nbsp;&nbsp;&nbsp;&nbsp;Mid Dancability :

> Mid Dance (red), mid-danceability tracks are the most common and have a wide range of popularity, while low-danceability tracks are the least common but can still be quite popular.

<h3>5. Energy</h3>

&nbsp;&nbsp;&nbsp;&nbsp;**Cluster the Energy**

|Cluster\_Energy|Energy|
|---|---|
|High\_Energy|0.7 - 1.0|
|Mid\_Energy|0.4 - 0.7|
|Low\_Energy|0.0 - 0.4|
- Measure of intensity and activity in the track, from 0.0 to 1.0.
 - Low Energy: 0.0 - 0.4 (e.g., acoustic, ambient, soft ballads)
 - Medium Energy: 0.4 - 0.7 (e.g., indie rock, chill electronic)
 - High Energy: 0.7 - 1.0 (e.g., EDM, rock, fast-paced pop)

<h3>Plot the graph</h3>

![newplot (8)](https://github.com/user-attachments/assets/ce593f60-0178-4b03-9b96-1ce4d6e2832a)

&nbsp;&nbsp;&nbsp;&nbsp;Mid Energy (red)

> The dataset is dominated by mid- and high-energy tracks, with high-energy tracks showing a concentration in the middle popularity range. Low-energy songs are less common but can achieve high popularity, with a notable spread in their popularity scores.

<h3>6.Loudness</h3>

&nbsp;&nbsp;&nbsp;&nbsp;**Cluster the Loudness**

|Cluster\_Loudness|Loudness|
|---|---|
|High\_Loud| > -11|
|Mid\_Loud| -14 > x < -11|
|Low\_Loud| < -14|
- Spotify offers three loudness settings to control how normalization is applied:

 - Loud : This applies a normalization level of around -11 dB LUFS, suitable for noisier environments where higher volume is needed.
 - Normal (default) : This is the standard setting at -14 dB LUFS, aiming for balanced playback across all tracks.
 - Quiet : This setting lowers the loudness normalization target to -23 dB LUFS, ideal for quiet environments or more dynamic listening experiences.

<h3>Plot the graph</h3>

![newplot (5)](https://github.com/user-attachments/assets/fed033df-3ca4-448e-969d-2edc55ce53a8)

&nbsp;&nbsp;&nbsp;&nbsp;High Loudness:

> The dataset is heavily skewed towards songs with high loudness, with a significant majority of tracks falling into this category. Mid- and low-loud tracks are much less common. This refers to tracks with a higher overall sound level.

<h3>7. Speechiness</h3>

&nbsp;&nbsp;&nbsp;&nbsp;**Cluster the Speechiness**

|Cluster\_Speechiness|Speechiness|
|---|---|
|High\_Speech| 0.666 - 1.0|
|Mid\_Speech|0.333 - 0.666|
|Low\_Speech|0.0 - 0.333 |
-  Detects the presence of spoken words in a track, from 0.0 to 1.0.
 - Low Speechiness: 0.0 - 0.333 (e.g., music without much spoken word)
 - Medium Speechiness: 0.333 - 0.666 (e.g., tracks with both music and speech, like rap)
 - High Speechiness: 0.666 - 1.0 (e.g., podcasts, spoken word tracks)

<h3>Plot the graph</h3>

![newplot (9)](https://github.com/user-attachments/assets/7ae4fa8a-5bb1-4b31-8cb3-d83844f6bbe8)

&nbsp;&nbsp;&nbsp;&nbsp;Low Speechiness (yellow):

> Scatter plot suggests that most popular songs don't have a high amount of spoken word content. Songs with more speech-like qualities (mid and high speechiness) are less common, and their popularity is more varied.

<h3>8. Acousticness</h3>

&nbsp;&nbsp;&nbsp;&nbsp;**Cluster the Acousticness**

|Cluster\_Acousticness|Acousticness|
|---|---|
|High\_Acoustic|0.7 - 1.0|
|Mid\_Acoustic|0.3 - 0.7|
|Low\_Acoustic| 0.0 - 0.3 |
- Confidence level that the track is acoustic, from 0.0 to 1.0.
 - Low Acousticness: 0.0 - 0.3 (e.g., electronic, heavily produced)
 - Medium Acousticness: 0.3 - 0.7 (e.g., some balance between acoustic and electronic elements)
 - High Acousticness: 0.7 - 1.0 (e.g., acoustic tracks, singer-songwriter)

<h3>Plot the graph</h3>

![newplot (10)](https://github.com/user-attachments/assets/e39cf834-84ce-4ffb-ac33-894abde0e670)

&nbsp;&nbsp;&nbsp;&nbsp;Low Acousticness (yellow):

> Most tracks in the dataset are less acoustic and more electronic or produced, and they tend to fall in the mid-to-high popularity range. As acousticness increases, the number of tracks decreases, and popularity tends to spread more evenly across a mid-level range.

<h3>9. Instrumentalness</h3>

&nbsp;&nbsp;&nbsp;&nbsp;**Cluster the Instrumentalness**

|Cluster\_Instrumentalness|Instrumentalness|
|---|---|
|High\_Instru| 0.5 - 1.0|
|Mid\_Instru|0.1 - 0.5|
|Low\_Instru| 0.0 - 0.1|
- Probability that the track contains no vocals, from 0.0 to 1.0.
 - Vocal-heavy: 0.0 - 0.1 (most mainstream music)
 - Medium Instrumentalness: 0.1 - 0.5 (vocals present but not dominant)
 - Instrumental: 0.5 - 1.0 (mostly instrumental, no vocals)

<h3>Plot the graph</h3>

![newplot (11)](https://github.com/user-attachments/assets/d0a91a32-9c64-4226-9869-5a35ee1bdeb6)

&nbsp;&nbsp;&nbsp;&nbsp;Low Instrumentalness (yellow):

> Most tracks have very low instrumentalness, meaning they likely include vocals and are more popular. Mid and high instrumentalness tracks (which likely have more instrumental content or no vocals) are far less common but can still achieve moderate popularity.

<h3>10. Liveness</h3>

&nbsp;&nbsp;&nbsp;&nbsp;**Cluster the Liveness**

|Cluster\_Liveness|Liveness|
|---|---|
|Studio_Liveness| 0.0 - 0.3|
|Outdoor_Liveness|0.3 - 1|
Detects the presence of a live audience in the recording, from 0.0 to 1.0. <br>

10.1.Studio quality group
 - Studio-like: 0.0 - 0.3 (recorded in a studio without live ambiance) <br>
 
10.2.Outdoor quality group
 - Medium Liveness: 0.3 - 0.6 (some audience noise or live characteristics)
 - Live Recording: 0.6 - 1.0 (recorded live in concert with audience presence)

<h3>Plot the graph</h3>

![newplot (13)](https://github.com/user-attachments/assets/1dc50313-3d18-43ac-bf09-76be75cb45ec)

&nbsp;&nbsp;&nbsp;&nbsp;Studio Liveness (light purple) :

> Most of the tracks in this dataset have low liveness,indicates these tracks are likely recorded in a studio setting. Tracks with higher liveness (more live-sounding or actual live recordings) are less common but can still achieve a wide range of popularity levels.

<h3>11. Valence</h3>

&nbsp;&nbsp;&nbsp;&nbsp;**Cluster the Valence**

|Cluster\_Valence|Valence|
|---|---|
|High\_Valence| 0.6 - 1.0|
|Mid\_Valence|0.3 - 0.6|
|Low\_Valence| 0.0 - 0.3|
- Describes the musical positiveness conveyed by a track, from 0.0 to 1.0.
 - Low Valence: 0.0 - 0.3 (e.g., sad, melancholic tracks)
 - Medium Valence: 0.3 - 0.6 (e.g., neutral or emotionally mixed tracks)
 - High Valence: 0.6 - 1.0 (e.g., happy, cheerful, upbeat tracks)

<h3>Plot the graph</h3>

![newplot (12)](https://github.com/user-attachments/assets/1b293f16-f220-4982-a5b6-f9758d7c4fb2)

&nbsp;&nbsp;&nbsp;&nbsp;Mid & High Valence :

> Mid- and high-valence tracks (positive or happy songs) dominate the dataset, and they tend to be quite popular, with most falling in the 60 to 80 popularity range.

<h3>12. Tempo</h3>

&nbsp;&nbsp;&nbsp;&nbsp;**Cluster the Tempo**

|Cluster\_Tempo|Tempo|
|---|---|
|High\_Tempo| 120 - 180+ BPM |
|Mid\_Tempo|60 - 120 BPM|
|Low\_Tempo| 0 - 60 BPM|
- Speed of the track in beats per minute (BPM).
 - Slow: 0 - 60 BPM (e.g., ballads, ambient music)
 - Medium: 60 - 120 BPM (e.g., pop, mid-tempo rock)
 - Fast: 120 - 180+ BPM (e.g., dance, EDM, upbeat tracks)

<h3>Plot the graph</h3>

![newplot (3)](https://github.com/user-attachments/assets/13e37899-67cc-41ad-b7e5-0e4146660463)

&nbsp;&nbsp;&nbsp;&nbsp;Mid & High Tempo

> Most of the tracks in this dataset are either mid-tempo or high-tempo, with a slight edge to the faster songs. Low-tempo tracks don’t seem to be represented at all.

<h3>13. Time Signature</h3> <br>
> Do not required clustering

<h3>Plot the graph</h3>

![newplot (1)](https://github.com/user-attachments/assets/b75c1d2e-1a45-4b4d-ab3a-86da65d16aaf)

&nbsp;&nbsp;&nbsp;&nbsp;4/4 Time Signature:

> The overwhelming majority of tracks (584) use the 4/4 time signature, while other time signatures like 3/4, 5/8, and 1/4 are used much less frequently, making them rare in the dataset. This reflects the dominance of the 4/4 signature in mainstream music.

<hr>

<h2>2. Find the most streamed genre on platform.</h2>

<h3>Announcing the "Popularity" value</h3>

&nbsp;&nbsp;&nbsp;&nbsp; **"Popularity"** refers to a metric provided by streaming platforms such as Spotify. It indicates how popular a track is based on a variety of factors, primarily:

1. **Recent Streaming Activity**: Popularity is often calculated based on how frequently a song has been streamed in a recent period (like the last few days or weeks).
2. **Lifetime Streams**: Although recent activity is a big part of popularity, the total number of streams a song has ever accumulated can also influence this score.
3. **Engagement Metrics**: These can include things like how many people save the song to their playlists, share it, or listen to it multiple times.
4. **Platform-Specific Factors**: Streaming services sometimes have internal algorithms that consider other factors, such as user interactions and geographical regions where the track is being played.

&nbsp;&nbsp;&nbsp;&nbsp; For example, in Spotify's API, the popularity of a track is expressed as a number from 0 to 100, with 100 being the most popular.

![newplot](https://github.com/user-attachments/assets/941b1b87-ee9b-46a0-aa66-d9e6a72e7f79)

> The *NaN* Data

&nbsp;&nbsp;&nbsp;&nbsp; The **Pop** genre is by far the most streamed on the platform, with a huge margin over other genres. But the presence of a significant number of *"Unknown"* labels affects the clarity of the data and should be noted when interpreting these results.

<br>

![newplot (1)](https://github.com/user-attachments/assets/66df5eef-6c5a-4966-8790-6116fd6d16c3)

> More clarify data

&nbsp;&nbsp;&nbsp;&nbsp; In this dataset, the *"Unknown"* label only accounts for 1.19 billion streams, which is much lower than in the first dataset. This gives us more confidence in the genre distribution and allows for more accurate conclusions.

&nbsp;&nbsp;&nbsp;&nbsp; From the "Streams by Genre" chart, we can clearly see that **Pop is the most dominant genre**, with a staggering 200.77 billion streams, making it far more popular than any other genre on the platform.

Other significant genres include:

 - **World/Traditional**, with 45.05 billion streams, and
 - **R&B/Soul**, with 26.11 billion streams.

These genres are still popular but are dwarfed by Pop's massive stream count.

<hr>

<h2>3. Does the artist's fame affect whether a song makes it onto the Billboard charts?</h2>

<h4>
  Let's highlight an important point about quality versus quantity when it comes to music tracks by artists.
</h4>

![newplot (16)](https://github.com/user-attachments/assets/ab5b443e-1611-470a-a3a6-c070d8793b5d)

&nbsp;&nbsp;&nbsp;&nbsp; **Artists with fewer tracks but high average popularity** (like J Balvin, Grupo Frontera, and Tyler Childers) suggest that, even though they release fewer songs, the songs they do release are very popular and well-received. This implies a focus on quality over quantity—the fewer songs they release tend to be hits, indicating that their music resonates strongly with listeners.

&nbsp;&nbsp;&nbsp;&nbsp; On the other hand, **artists with more tracks but lower average popularity** (like Latto and Lizzo) might indicate that their popularity is driven more by their overall fame and brand as artists, rather than the quality of each individual song. While they produce a larger volume of music, not every track necessarily becomes a standout hit. This could imply that their success may rely more on their established name rather than consistently high-performing songs.

<hr>

<h1 align=center>Refined work resulting from the analytical process</h1>

<h2> Lets create a song !! </h2>

> Key: B Major , Time sig : 4/4 , Tempo 125bpm , 3.5 mins , mid-high loudness , Danceable , Energetic , More Instumental , Electronic Pop , Mid - High Valence

**Kokoro no Uta**

![image](https://github.com/user-attachments/assets/a6d2fd97-800e-410d-b384-74f22a56e657)

https://suno.com/song/2c69627f-5e20-40de-a4dd-41f70f28fb53

(Generated by : [suno.com](https://suno.com/))

<hr>

<h1>Challenges</h1>

<h3>Low Correlation</h3>

![newplot (18)](https://github.com/user-attachments/assets/7cc5cf31-31e4-47d7-8deb-392b564a23ad)

 - **Speechiness** has the *strongest negative correlation (-0.22)*, suggesting that songs with more speech-like characteristics tend to be less popular.<br>
 - Other features, such as **Duration** and **Acousticness**, show *weak positive correlations* with Popularity, while **Energy**, **Valence**, and **Loudness** show *weak negative correlations*.

<h3>Different collecting method from each data</h3>

 - Each data collection from different method, resulting in format of name of song and artist contain capitalized letter and there're some unexpected **space" "**. This caused tons of duplication in data after the merging process, the cleaning process heavily required.

<hr>

<h1>Further Steps</h1>

 - To get a clearer picture, running a regression analysis can help to visualize how much of the variation in Popularity is explained by these features.<br>
 - Interactions between variables to understand non-linear relationships and more of data.<br>
 - Time-Series Analysis, study how music trends evolve over time based on track release years). <br>
 -  Playlist Creation Analysis, examine which track features are more likely to land a song on popular playlists.<br>
 -  **For further study, including more additional datasets, such as marketing data, to analyze more factors that contribute to a song's potential for becoming popular.**

<hr>
