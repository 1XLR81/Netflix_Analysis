# Netflix-Analysis

## Description
This project analyzes Netflix's shows and movies dataset to extract meaningful insights for subscribers. Using SQL and MySQL, the project uncovers trends in viewer ratings, popularity, genre preferences, and content distribution across decades and age certifications. The analysis addresses Netflix's challenge of handling large datasets to provide actionable insights for content recommendations and audience preferences.

## Business Problem
Netflix aims to derive valuable insights from their extensive shows and movies dataset to enhance subscriber experience. With approximately 82,000 rows of data, the challenge lies in effectively analyzing this vast dataset to uncover patterns and trends. The goal is to provide a scalable data analytics solution to identify viewer preferences, content performance, and strategic opportunities for content curation.

## Datasets Used
![DATASET]((https://www.kaggle.com/datasets/victorsoeiro/netflix-tv-shows-and-movies?select=titles.csv))

The dataset includes Netflix's shows and movies data, with approximately 82,000 rows, containing attributes such as:
- Title
- Type (Movie or Show)
- IMDB Score
- TMDB Score
- Release Year
- Age Certification
- Genres

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
  **Result**: [Q1 - Placeholder for results]

- **Top 10 Shows**:
  ```sql
  SELECT title,
  type, imdb_score
  FROM Netflix_data
  WHERE type = 'SHOW'
  ORDER BY imdb_score DESC
  LIMIT 10
  ```
  **Result**: [Q2 - Placeholder for results]

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
  **Result**: [Q3 - Placeholder for results]

-**Bottom 10 Shows**:
  ```sql
  SELECT title, type, imdb_score
  FROM shows_movies.titles
  WHERE type = 'SHOW'
  ORDER BY imdb_score ASC
  LIMIT 10;
  ```
  **Result**: [Q4 - Placeholder for results]

**Insights**: The top 10 movies and shows, with IMDB scores ≥ 8.0, are highly regarded, indicating strong viewer approval. Conversely, the bottom 10 titles reveal lower audience reception, potentially due to factors like weak plots or production quality. These findings guide content recommendations and highlight areas for improvement.

### 2. Distribution of Movies and Shows by Decade
**Objective**: Analyze the number of titles per decade to understand Netflix’s content distribution over time.

```sql
SELECT CONCAT(FLOOR(release_year / 10) * 10, 's') AS decade,
       COUNT(*) AS movies_shows_count
FROM shows_movies.titles
WHERE release_year >= 1940
GROUP BY CONCAT(FLOOR(release_year / 10) * 10, 's')
ORDER BY decade;
```
**Result**: [Q5 - Placeholder for results]

**Insights**: The analysis shows a significant increase in content from the 2000s onward, with 3,304 titles in the 2010s and 1,972 in the 2020s (ongoing). Earlier decades (1940s–1980s) have fewer titles, while the 1990s mark a surge with 121 titles. This reflects Netflix’s focus on contemporary content aligned with current trends.

### 3. Impact of Age Certifications
**Objective**: Examine how age certifications influence IMDB and TMDB scores and their distribution in the dataset.

- **Average Scores by Age Certification**:
  ```sql
  SELECT DISTINCT age_certification, 
         ROUND(AVG(imdb_score),2) AS avg_imdb_score,
         ROUND(AVG(tmdb_score),2) AS avg_tmdb_score
  FROM shows_movies.titles
  GROUP BY age_certification
  ORDER BY avg_imdb_score DESC;
  ```
  **Result**: [Q6 - Placeholder for results]

- **Distribution of Age Certifications for Movies**:
  ```sql
  SELECT age_certification, 
         COUNT(*) AS certification_count
  FROM shows_movies.titles
  WHERE type = 'Movie' 
  AND age_certification != 'N/A'
  GROUP BY age_certification
  ORDER BY certification_count DESC
  LIMIT 5;
  ```
  **Result**: [Q7 - Placeholder for results]

**Insights**: TV-14 content has the highest average IMDB score (6.71), indicating strong viewer preference. R-rated titles are the most prevalent (556 movies), followed by PG-13 (451). TV-G and TV-Y content also perform well, while NC-17 is least represented (16 titles). This highlights Netflix’s diverse content range catering to varied audiences.

### 4. Most Common Genres
**Objective**: Identify the most frequent genres for movies, shows, and overall to understand viewer preferences.

- **Top 10 Genres for Movies**:
  ```sql
  SELECT genres, 
         COUNT(*) AS title_count
  FROM shows_movies.titles 
  WHERE type = 'Movie'
  GROUP BY genres
  ORDER BY title_count DESC
  LIMIT 10;
  ```
  **Result**: [Q8 - Placeholder for results]

- **Top 10 Genres for Shows**:
  ```sql
  SELECT genres, 
         COUNT(*) AS title_count
  FROM shows_movies.titles 
  WHERE type = 'Show'
  GROUP BY genres
  ORDER BY title_count DESC
  LIMIT 10;
  ```
  **Result**: [Q9 - Placeholder for results]

- **Top 3 Genres Overall**:
  ```sql
  SELECT t.genres, 
         COUNT(*) AS genre_count
  FROM shows_movies.titles AS t
  WHERE t.type = 'Movie' or t.type = 'Show'
  GROUP BY t.genres
  ORDER BY genre_count DESC
  LIMIT 3;
  ```
  **Result**: [Q10 - Placeholder for results]

**Insights**: Comedy dominates with 484 titles, followed by documentation (329) and drama (328). Multi-genre combinations (e.g., comedy + drama) are also popular, reflecting Netflix’s diverse offerings. Reality and drama lead for shows, while comedy and documentation are prevalent for movies.

## SQL Queries
The SQL queries used in this analysis are included above with their respective questions. They leverage MySQL to filter, aggregate, and sort data, enabling insights into ratings, decades, certifications, and genres.

## Conclusion
This analysis provides a comprehensive view of Netflix’s content landscape:
- **IMDB Scores**: Top-rated titles (scores ≥ 8.0) guide recommendations, while low-rated titles highlight areas for improvement.
- **Decades**: A surge in content from the 2000s (3,304 titles in 2010s, 1,972 in 2020s) shows Netflix’s focus on modern content.
- **Age Certifications**: TV-14 content scores highest (6.71), with R and PG-13 being most common, reflecting diverse audience appeal.
- **Genres**: Comedy (484 titles), documentation (329), and drama (328) dominate, with multi-genre content also popular.

These insights help Netflix understand viewer preferences, optimize content curation, and enhance subscriber experience. The project demonstrates the power of SQL for handling large datasets and extracting actionable trends.

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/username/Netflix-SQL-Analysis.git
   ```
2. Navigate to the project directory:
   ```bash
   cd Netflix-SQL-Analysis
   ```
3. Set up MySQL:
   - Install MySQL if not already installed.
   - Import the dataset into MySQL (update with specific dataset import instructions if available).
4. Install dependencies (if applicable):
   ```bash
   pip install -r requirements.txt
   ```
   *Note*: Update with specific dependencies if Excel or other tools require them.

## Usage
1. Run the SQL queries in MySQL Workbench or a similar environment.
2. Use the provided `.sql` files (if included) or copy-paste queries from this README.
3. Analyze results to derive insights or visualize using Excel or other tools.
4. Example command to execute a query:
   ```sql
   mysql -u username -p shows_movies < query.sql
   ```

## Contributing
Contributions are welcome! To contribute:
1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Make changes and commit (`git commit -m 'Add new feature'`).
4. Push to the branch (`git push origin feature-branch`).
5. Create a Pull Request.

## License
This project is licensed under the [MIT License](LICENSE) - see the LICENSE file for details.

## Contact
For questions or support:
- Email: your.email@example.com
- GitHub: [Your GitHub Profile](https://github.com/username)
- Project Issues: [GitHub Issues](https://github.com/username/Netflix-SQL-Analysis/issues)

## Visual
![Netflix Analysis Visualization](path/to/visualization.png)
*Note*: Replace `path/to/visualization.png` with the actual path to your project’s visualization or screenshot.
