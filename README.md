<h1>Introducing Dataset</h1>
lorem

&nbsp;&nbsp;&nbsp;&nbsp; The dataset offers a detailed overview of contemporary music, featuring 620 tracks from 87 chart-topping artists between 2000 and 2023. It highlights the diversity of modern pop and R&B, capturing the evolution of Hot 100 hits over two decades. Each track is annotated with Spotify's audio features, providing insights into characteristics like tempo, energy, danceability, and valence, making it a valuable resource for exploring trends in popular music.

<h1>Key finding</h1>

Working on Spotify's api data
1. Visualize characteristics of hit songs on Billboard charts.
2. Find the most streamed genre on platform.
3. Does the artist's fame affect whether a song makes it onto the Billboard charts?

<h1>What is "Billboard" and Why "Spotify"</h1>
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

<h1>Clustering Data</h1>

**1. Key**
*   Musical key of the track, represented by integers (0 = C, 1 = C#/Db, etc.).

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


**2. Mode**
* Indicates whether the track is in a major (1) or minor (0) key.

|Cluster\_Mode|Mode|
|---|---|
|Minor|0|
|Major|1|

**3. Duration**
- Length of the track, usually in milliseconds.
 - Short: 0 - 180,000 ms (0 - 3 minutes)
 - Medium: 180,001 - 300,000 ms (3 - 5 minutes)
 - Long: 300,001 ms and above (5+ minutes)

|Cluster\_Duration\(Min\)|Duration|
|---|---|
|0-3mins|0 - 180,000 ms|
|3-5mins|180,001 - 300,000 ms|
|5+mins|300,001 ms and above |

**4. Danceability**
- How suitable a track is for dancing, from 0.0 to 1.0.
 - Low: 0.0 - 0.4 (e.g., classical, ambient)
 - Medium: 0.4 - 0.7 (e.g., soft rock, indie)
 - High: 0.7 - 1.0 (e.g., pop, dance, hip-hop)

|Cluster\_Danceability|Danceability|
|---|---|
|High\_Dance| 0.7 - 1.0|
|Mid\_Dance|0.4 - 0.7|
|Low\_Dance| 0.0 - 0.4|

**5. Energy**
- Measure of intensity and activity in the track, from 0.0 to 1.0.
 - Low Energy: 0.0 - 0.4 (e.g., acoustic, ambient, soft ballads)
 - Medium Energy: 0.4 - 0.7 (e.g., indie rock, chill electronic)
 - High Energy: 0.7 - 1.0 (e.g., EDM, rock, fast-paced pop)

|Cluster\_Energy|Energy|
|---|---|
|High\_Energy|0.7 - 1.0|
|Mid\_Energy|0.4 - 0.7|
|Low\_Energy|0.0 - 0.4|

**6.Loudness**
- Spotify offers three loudness settings to control how normalization is applied:

 - Loud : This applies a normalization level of around -11 dB LUFS, suitable for noisier environments where higher volume is needed.
 - Normal (default) : This is the standard setting at -14 dB LUFS, aiming for balanced playback across all tracks.
 - Quiet : This setting lowers the loudness normalization target to -23 dB LUFS, ideal for quiet environments or more dynamic listening experiences.

|Cluster\_Loudness|Loudness|
|---|---|
|High\_Loud| > -11|
|Mid\_Loud| -14 > x < -11|
|Low\_Loud| < -14|

**7. Speechiness**
-  Detects the presence of spoken words in a track, from 0.0 to 1.0.
 - Low Speechiness: 0.0 - 0.333 (e.g., music without much spoken word)
 - Medium Speechiness: 0.333 - 0.666 (e.g., tracks with both music and speech, like rap)
 - High Speechiness: 0.666 - 1.0 (e.g., podcasts, spoken word tracks)

|Cluster\_Speechiness|Speechiness|
|---|---|
|High\_Speech| 0.666 - 1.0|
|Mid\_Speech|0.333 - 0.666|
|Low\_Speech|0.0 - 0.333 |

**8. Acousticness**
- Confidence level that the track is acoustic, from 0.0 to 1.0.
 - Low Acousticness: 0.0 - 0.3 (e.g., electronic, heavily produced)
 - Medium Acousticness: 0.3 - 0.7 (e.g., some balance between acoustic and electronic elements)
 - High Acousticness: 0.7 - 1.0 (e.g., acoustic tracks, singer-songwriter)

|Cluster\_Acousticness|Acousticness|
|---|---|
|High\_Acoustic|0.7 - 1.0|
|Mid\_Acoustic|0.3 - 0.7|
|Low\_Acoustic| 0.0 - 0.3 |

**9. Instrumentalness**
- Probability that the track contains no vocals, from 0.0 to 1.0.
 - Vocal-heavy: 0.0 - 0.1 (most mainstream music)
 - Medium Instrumentalness: 0.1 - 0.5 (vocals present but not dominant)
 - Instrumental: 0.5 - 1.0 (mostly instrumental, no vocals)

|Cluster\_Instrumentalness|Instrumentalness|
|---|---|
|High\_Instru| 0.5 - 1.0|
|Mid\_Instru|0.1 - 0.5|
|Low\_Instru| 0.0 - 0.1|

**10. Liveness**
Detects the presence of a live audience in the recording, from 0.0 to 1.0. <br>

10.1.Studio quality group
 - Studio-like: 0.0 - 0.3 (recorded in a studio without live ambiance) <br>
 
10.2.Outdoor quality group
 - Medium Liveness: 0.3 - 0.6 (some audience noise or live characteristics)
 - Live Recording: 0.6 - 1.0 (recorded live in concert with audience presence)

|Cluster\_Liveness|Liveness|
|---|---|
|Studio_Liveness| 0.0 - 0.3|
|Outdoor_Liveness|0.3 - 1|

**11. Valence**
- Describes the musical positiveness conveyed by a track, from 0.0 to 1.0.
 - Low Valence: 0.0 - 0.3 (e.g., sad, melancholic tracks)
 - Medium Valence: 0.3 - 0.6 (e.g., neutral or emotionally mixed tracks)
 - High Valence: 0.6 - 1.0 (e.g., happy, cheerful, upbeat tracks)

|Cluster\_Valence|Valence|
|---|---|
|High\_Valence| 0.6 - 1.0|
|Mid\_Valence|0.3 - 0.6|
|Low\_Valence| 0.0 - 0.3|

**12. Tempo**
- Speed of the track in beats per minute (BPM).
 - Slow: 0 - 60 BPM (e.g., ballads, ambient music)
 - Medium: 60 - 120 BPM (e.g., pop, mid-tempo rock)
 - Fast: 120 - 180+ BPM (e.g., dance, EDM, upbeat tracks)

|Cluster\_Tempo|Tempo|
|---|---|
|High\_Tempoe| 120 - 180+ BPM |
|Mid\_Tempo|60 - 120 BPM|
|Low\_Tempo| 0 - 60 BPM|

**13. Time Signature** <br>
<p>Do not required clustering</p>

<hr>



<h2>1. Visualize characteristics of hit songs on Billboard charts.</h2>

<h3>Key Signature</h3>

![newplot](https://github.com/user-attachments/assets/0a3515db-6d85-4f76-bde0-336cb21d78c7)

B , C and C#/Db :

> The keys B, C, and C#/Db dominate this dataset, while Eb and A#/Bb are the least represented. It seems the dataset leans heavily on certain keys while others are used less frequently.

<h3>Time Signature</h3>

![newplot (1)](https://github.com/user-attachments/assets/b75c1d2e-1a45-4b4d-ab3a-86da65d16aaf)

4/4 Time Signature:

> The overwhelming majority of tracks (584) use the 4/4 time signature, while other time signatures like 3/4, 5/8, and 1/4 are used much less frequently, making them rare in the dataset. This reflects the dominance of the 4/4 signature in mainstream music.

<h3>Major or Minor</h3>

![newplot (2)](https://github.com/user-attachments/assets/b48fb2e5-7ed3-47a2-87b7-9827cabdfc9d)

Major Mode:
> Most songs in the dataset are in a major key, making up almost two-thirds of the total. A smaller chunk, just over a third, are in a minor key, which tends to give songs a different, more emotional vibe.

<h3> Tempo</h3>

![newplot (3)](https://github.com/user-attachments/assets/13e37899-67cc-41ad-b7e5-0e4146660463)

Mid & High Tempo

> Most of the tracks in this dataset are either mid-tempo or high-tempo, with a slight edge to the faster songs. Low-tempo tracks don’t seem to be represented at all.

<h3> Duration </h3> 

![newplot (4)](https://github.com/user-attachments/assets/c9060aa4-32c9-47ee-a799-8df729eeb141)

3-5 minutes song :

> Tracks between 3-5 minutes dominate. The majority of the tracks, 462 in total, fall within the 3-5 minute range. This indicates that most tracks in the dataset are of moderate length, which is a common duration for popular music.

<h3> Loudness </h3>

![newplot (5)](https://github.com/user-attachments/assets/fed033df-3ca4-448e-969d-2edc55ce53a8)

High Loudness:

> The dataset is heavily skewed towards songs with high loudness, with a significant majority of tracks falling into this category. Mid- and low-loud tracks are much less common. This refers to tracks with a higher overall sound level.

<h3> Danceability </h3>

![newplot (6)](https://github.com/user-attachments/assets/bc7b53c0-cfbc-423d-866c-146ce89d5681)

Mid Dancability :

> Mid Dance (red), mid-danceability tracks are the most common and have a wide range of popularity, while low-danceability tracks are the least common but can still be quite popular.

<h3> Energy </h3>

![newplot (8)](https://github.com/user-attachments/assets/ce593f60-0178-4b03-9b96-1ce4d6e2832a)

Mid Energy (red)

> The dataset is dominated by mid- and high-energy tracks, with high-energy tracks showing a concentration in the middle popularity range. Low-energy songs are less common but can achieve high popularity, with a notable spread in their popularity scores.

<h3> Speechiness</h3>

![newplot (9)](https://github.com/user-attachments/assets/7ae4fa8a-5bb1-4b31-8cb3-d83844f6bbe8)

Low Speechiness (yellow):

> Scatter plot suggests that most popular songs don't have a high amount of spoken word content. Songs with more speech-like qualities (mid and high speechiness) are less common, and their popularity is more varied.

<h3> Acouticness</h3>

![newplot (10)](https://github.com/user-attachments/assets/e39cf834-84ce-4ffb-ac33-894abde0e670)

Low Acousticness (yellow):

> Most tracks in the dataset are less acoustic and more electronic or produced, and they tend to fall in the mid-to-high popularity range. As acousticness increases, the number of tracks decreases, and popularity tends to spread more evenly across a mid-level range.

<h3> Instrumentalness</h3>

![newplot (11)](https://github.com/user-attachments/assets/d0a91a32-9c64-4226-9869-5a35ee1bdeb6)

Low Instrumentalness (yellow):

> Most tracks have very low instrumentalness, meaning they likely include vocals and are more popular. Mid and high instrumentalness tracks (which likely have more instrumental content or no vocals) are far less common but can still achieve moderate popularity.

<h3> Valence</h3>

![newplot (12)](https://github.com/user-attachments/assets/1b293f16-f220-4982-a5b6-f9758d7c4fb2)

Mid & High Valence :

> Mid- and high-valence tracks (positive or happy songs) dominate the dataset, and they tend to be quite popular, with most falling in the 60 to 80 popularity range.

<h3> Liveness</h3>

![newplot (13)](https://github.com/user-attachments/assets/1dc50313-3d18-43ac-bf09-76be75cb45ec)

Studio Liveness (light purple) :

> Most of the tracks in this dataset have low liveness,indicates these tracks are likely recorded in a studio setting. Tracks with higher liveness (more live-sounding or actual live recordings) are less common but can still achieve a wide range of popularity levels.

<hr>

<h2>2. Find the most streamed genre on platform.</h2>

![newplot (14)](https://github.com/user-attachments/assets/35ad2e04-b9c9-421c-8428-e6ed70ceb0e9)

> The *NaN* Data

&nbsp;&nbsp;&nbsp;&nbsp; The **Pop** genre is by far the most streamed on the platform, with a huge margin over other genres. But the presence of a significant number of *"Unknown"* labels affects the clarity of the data and should be noted when interpreting these results.

<br>

![newplot (17)](https://github.com/user-attachments/assets/23f16954-1b47-43b6-b0ab-628694e67849)

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














