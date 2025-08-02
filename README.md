# Netflix-Analysis

## Description
This project analyzes Netflix's shows and movies dataset to extract meaningful insights for subscribers. Using SQL and MySQL, the project uncovers trends in viewer ratings, popularity, genre preferences, and content distribution across decades and age certifications. The analysis addresses Netflix's challenge of handling large datasets to provide actionable insights for content recommendations and audience preferences.

## Business Problem
Netflix aims to derive valuable insights from their extensive shows and movies dataset to enhance subscriber experience. With vast data, the challenge lies in effectively analyzing this vast dataset to uncover patterns and trends. The goal is to provide a scalable data analytics solution to identify viewer preferences, content performance, and strategic opportunities for content curation.

## Datasets Used
![DATASET]((https://www.kaggle.com/datasets/victorsoeiro/netflix-tv-shows-and-movies?select=titles.csv))


## Analysis and Findings
This project addresses the following key questions to uncover insights from the Netflix dataset:

### 1. Top and Bottom 10 Movies and Shows by IMDB Scores
**Objective**: Identify the highest and lowest-rated movies and shows based on IMDB scores to understand content quality and audience reception.

- **Top 10 Movies**:
  ```sql
  SELECT title,
  type,
  imdb_score
  FROM Netflix_data
  WHERE type = 'MOVIE'
  ORDER BY imdb_score DESC
  LIMIT 10
  ```


- **Top 10 Shows**:
  ```sql
  SELECT title,
  type, imdb_score
  FROM Netflix_data
  WHERE type = 'SHOW'
  ORDER BY imdb_score DESC
  LIMIT 10
  ```
 

- **Bottom 10 Movies**:
  ```sql
  """
  SELECT title, type, imdb_score
  FROM Netflix_data
  WHERE type = 'MOVIE'
  ORDER BY imdb_score ASC
  LIMIT 10
"""
  ```
-**Bottom 10 Shows**:
  ```sql
  SELECT title, 
type, 
imdb_score
FROM Netflix_data
WHERE type = 'SHOW'
ORDER BY imdb_score ASC
LIMIT 10
  ```


**Insights**: The top 10 movies and shows, with higher IMDB scores, are highly regarded, indicating strong viewer approval. Conversely, the bottom 10 titles reveal lower audience reception, potentially due to factors like weak plots or production quality. These findings guide content recommendations and highlight areas for improvement.

### 2. Distribution of Movies and Shows by Decade
**Objective**: Analyze the number of titles per decade to understand Netflix’s content distribution over time.

```sql
SELECT CONCAT(FLOOR(release_year / 10) * 10, 's') AS decade,
	COUNT(*) AS movies_shows_count
FROM Netflix_data
WHERE release_year >= 1940
GROUP BY CONCAT(FLOOR(release_year / 10) * 10, 's')
ORDER BY decade;
```


**Insights**: The analysis shows a significant increase in content from the 2000s onward, with 3,304 titles in the 2010s and 1,972 in the 2020s (ongoing). Earlier decades (1940s–1980s) have fewer titles, while the 1990s mark a surge with 121 titles. This reflects Netflix’s focus on contemporary content aligned with current trends.

### 3. Impact of Age Certifications
**Objective**: Examine how age certifications influence IMDB and TMDB scores and their distribution in the dataset.

- **Average Scores by Age Certification**:
  ```sql
  SELECT DISTINCT age_certification,
  ROUND(AVG(imdb_score),2) AS avg_imdb_score,
  ROUND(AVG(tmdb_score),2) AS avg_tmdb_score
  FROM Netflix_data
  GROUP BY age_certification
  ORDER BY avg_imdb_score DESC
  ```
 

- **Distribution of Age Certifications for Movies**:
  ```sql
  SELECT age_certification,
  COUNT(*) AS certification_count
  FROM Netflix_data
  WHERE type = 'MOVIE'
  AND age_certification != 'N/A'
  GROUP BY age_certification
  ORDER BY certification_count DESC
  LIMIT 5;
  ```
  

**Insights**: TV-14 lead with the highest average IMDb and TMDb scores of 7.17, indicating strong viewer appreciation for content suitable for those aged 14 and older, likely due to its balance of mature themes and broad appeal. TV-PG and TV-Y7 follow with scores of 6.88 and 6.81, respectively, reflecting solid reception for family-friendly content, while TV-Y, TV-MA, PG-13, G, TV-G, R, and PG range from 6.54 to 6.24, showing varied but positive feedback. NC-17 titles score lowest at 6.17, likely due to their niche, mature nature.

When examining the distribution of movies and shows across age certifications,TV-MA dominates with 2,364 titles, underscoring Netflix’s focus on mature audiences, followed by R (556 titles) and PG-13 (451 titles), catering to teens and adults. PG (233 titles) and G (124 titles) provide family-friendly options, while NC-17 is least common with only 16 titles, reflecting its limited appeal. 

These insights highlight Netflix’s strategy of prioritizing mature content while offering high-quality, broadly appealing titles, particularly for TV-14 and TV-PG audiences.

### 4. Most Common Genres
**Objective**: Identify the most frequent genres for movies, shows, and overall to understand viewer preferences.

- **Top 10 Genres for Movies**:
  ```sql
  SELECT genres,
  COUNT(*) AS title_count
  FROM Netflix_data
  WHERE type = 'MOVIE'
  GROUP BY genres
  ORDER BY title_count DESC
  LIMIT 10;
  ```
 

- **Top 10 Genres for Shows**:
  ```sql
  SELECT genres,
  COUNT(*) AS title_count
  FROM Netflix_data
  WHERE type = 'SHOW'
  GROUP BY genres
  ORDER BY title_count DESC
  LIMIT 10;
  ```
  

- **Top 3 Genres Overall**:
  ```sql
  SELECT genres,
  COUNT(*) AS title_count
  FROM Netflix_data
  WHERE type = 'MOVIE' OR type='SHOW'
  GROUP BY genres
  ORDER BY title_count DESC
  LIMIT 3;
  ```
 

**Insights**: By analyzing the frequency of genres, we can gain a better understanding of the content that dominates the platform and the preferences of its audience. Starting with movies, the first query reveals the top 10 most common genres. Comedy emerges as the most popular genre with a total of 384 movies, reflecting its widespread appeal. Following closely behind are documentation with 230 movies and drama with 224 movies, indicating the significance of these genres in Netflix's movie collection. Combinations of genres also feature prominently, with comedy + documentation and comedy + drama occupying the fourth and fifth positions respectively. The presence of drama + romance, drama + comedy, and comedy + romance further emphasizes the audience's likeness for movies that blend multiple genres. These findings highlight the diverse range of movie genres available on Netflix and the platform's commitment to catering to a wide array of preferences.

Shifting the focus, the second query presents the top 10 most common genres for shows. Reality takes the lead with 113 shows, showcasing the popularity of this genre among Netflix viewers. Drama follows closely behind with 104 shows. Comedy and documentation also emerge as prevalent genres with 100 shows each. Similar to movies, combinations of genres such as comedy + drama and drama + romance are present, indicating viewer interest in multi-genre shows.

Combining the results from both movies and shows, the third query provides an overview of the top three most common genres overall. Comedy takes the lead with a total of 484 entries, reaffirming its position as a very popular genre among Netflix subscribers. Documentation follows closely behind with 329 entries, reflecting the popularity of informative content. Finally, drama secures the third spot with 328 entries. Overall, these findings shed light on the genres that dominate Netflix's library, showcasing the platform's efforts to cater to a diverse range of viewer preferences.

## SQL Queries
The SQL queries used in this analysis are included above with their respective questions. They leverage MySQL to filter, aggregate, and sort data, enabling insights into ratings, decades, certifications, and genres.

## Conclusion
This analysis provides a comprehensive view of Netflix’s content landscape:
- **IMDB Scores**: Top-rated titles guide recommendations, while low-rated titles highlight areas for improvement.
- **Decades**: A surge in content from the 2000s (3,304 titles in 2010s, 1,972 in 2020s) shows Netflix’s focus on modern content.
- **Age Certifications**: TV-14 content scores highest (7.17), with TV-MA and R being most common, reflecting diverse audience appeal.
- **Genres**: Comedy (484 titles), documentation (329), and drama (328) dominate, with multi-genre content also popular.

These insights help Netflix understand viewer preferences, optimize content curation, and enhance subscriber experience. The project demonstrates the power of SQL for handling large datasets and extracting actionable trends.

