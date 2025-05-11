

1. Count the number of Movies vs TV Shows  
   Purpose:  
   To find the total count of movies and TV shows in the dataset.  
   Explanation:  
   - DISTINCT type: Identifies the unique types (Movie and TV Show) in the dataset.  
   - COUNT(*): Counts the total number of rows for each type.  
   - GROUP BY type: Groups the data by type to ensure counts are calculated separately for each type.  

2. Find the most common rating for Movies and TV Shows  
   Purpose:  
   To determine which rating (e.g., PG, TV-MA) appears most frequently for movies and TV shows.  
   Explanation:  
   - COUNT(*): Counts the occurrences of each rating for movies and TV shows.  
   - RANK() OVER(PARTITION BY type ORDER BY COUNT(*) DESC): Creates a ranking for ratings based on their count, grouped by type (Movie or TV Show).  
   - WHERE ranking = 1: Filters the data to display only the most frequent rating for each type.  

3. List all movies released in a specific year (e.g., 2020)  
   Purpose:  
   To list all movies released in a given year, such as 2020.  
   Explanation:  
   - type = 'Movie': Filters the dataset to include only movies.  
   - release_year = 2020: Further filters the dataset to include only those movies released in 2020.  

4. Find the top 5 countries with the most content on Netflix  
   Purpose:  
   To identify the countries producing the most Netflix content.  
   Explanation:  
   - STRING_TO_ARRAY(country, ','): Splits the country field (which may contain multiple countries separated by commas) into an array of individual countries.  
   - UNNEST(): Expands the array into individual rows for easier counting.  
   - COUNT(show_id): Counts the number of content items for each country.  
   - GROUP BY: Groups data by each unique country.  
   - ORDER BY total_content DESC: Sorts the results in descending order to display countries with the highest content count first.  
   - LIMIT 5: Limits the result to the top 5 countries.  

5. Identify the longest movie  
   Purpose:  
   To find the movie with the longest duration in the dataset.  
   Explanation:  
   - type = 'Movie': Ensures only movies are considered.  
   - MAX(duration): Finds the longest duration value in the duration column.  

6. Find content added in the last 5 years  
   Purpose:  
   To retrieve all content added to Netflix within the last 5 years.  
   Explanation:  
   - TO_DATE(date_added, 'Month DD, YYYY'): Converts the date_added field (stored as text) into a proper date format.  
   - CURRENT_DATE - INTERVAL '5 years': Calculates the date 5 years ago from today.  
   - >=: Compares the converted date_added to the calculated date to include only recent content.  

7. Find all Movies/TV Shows by director 'Rajiv Chilaka'  
   Purpose:  
   To find all movies or TV shows directed by a specific person.  
   Explanation:  
   - director LIKE '%Rajiv Chilaka%': Searches for any content where the director field contains the name 'Rajiv Chilaka' (case-sensitive).  

8. List all TV shows with more than 5 seasons  
   Purpose:  
   To identify TV shows with more than 5 seasons.  
   Explanation:  
   - type = 'TV Show': Filters the dataset to include only TV shows.  
   - SPLIT_PART(duration, ' ', 1): Splits the duration field (e.g., "5 Seasons") and extracts the first part (e.g., "5").  
   - ::numeric > 5: Converts the extracted value to a numeric type and checks if it is greater than 5.  

9. Count the number of content items in each genre  
   Purpose:  
   To count how many content items belong to each genre.  
   Explanation:  
   - STRING_TO_ARRAY(listed_in, ','): Splits the listed_in column (which may have multiple genres separated by commas) into an array.  
   - UNNEST(): Breaks the array into individual rows.  
   - COUNT(show_id): Counts the number of content items for each genre.  

10. Find each year and the average number of content releases in India  
   Purpose:  
   To calculate the average content released each year in India and display the top 5 years.  
   Explanation:  
   - TO_DATE(date_added, 'Month DD, YYYY'): Converts date_added to a proper date format.  
   - EXTRACT(YEAR FROM TO_DATE(...)): Extracts the year from the date_added column.  
   - COUNT(*): Counts the total content released each year.  
   - ROUND(COUNT(*) / total_india_content, 2): Calculates the average release percentage for each year, rounded to two decimal places.  
   - LIMIT 5: Returns the top 5 years with the highest average content release.  

11. List all movies that are documentaries  
   Purpose:  
   To find all movies categorized as documentaries.  
   Explanation:  
   - type = 'Movie': Ensures only movies are included.  
   - listed_in LIKE '%Documentaries%': Filters content where the listed_in column mentions 'Documentaries.'  

12. Find all content without a director  
   Purpose:  
   To identify content where the director is not listed.  
   Explanation:  
   - director IS NULL: Filters rows where the director field is empty or missing.  

13. Find how many movies actor 'Salman Khan' appeared in the last 10 years  
   Purpose:  
   To find movies featuring Salman Khan released in the last 10 years.  
   Explanation:  
   - casts ILIKE '%Salman Khan%': Searches for 'Salman Khan' in the casts column (case-insensitive).  
   - release_year > (current_year - 10): Filters content released in the last 10 years.  

14. Find the top 10 actors who appeared in the most movies produced in India  
   Purpose:  
   To identify the most frequent actors in Indian movies.  
   Explanation:  
   - STRING_TO_ARRAY(casts, ','): Splits the casts column into individual actor names.  
   - UNNEST(): Expands the array of actor names into individual rows.  
   - COUNT(*): Counts the number of movies for each actor.  
   - ORDER BY total_content DESC: Sorts actors by the number of movies they appeared in, in descending order.  
   - LIMIT 10: Returns the top 10 actors.  

15. Categorize content based on the presence of keywords 'kill' and 'violence'  
   Purpose:  
   To label content as "Bad Content" if the description contains words like 'kill' or 'violence'; otherwise, label it as "Good Content."  
   Explanation:  
   - CASE: Defines conditions to categorize content.  
   - ILIKE '%kill%' OR ILIKE '%violence%': Checks if the description contains the keywords (case-insensitive).  
   - COUNT(*): Counts the total number of items in each category.  

