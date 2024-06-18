# data-sourcing-challenge
A movie recommendation system

This project involves preparing data for a movie recommendation system. The goal is to help users find movie reviews and related movies by extracting and merging data from two different sources: The New York Times API and The Movie Database (TMDb) API. The text extracted from these APIs will be used to improve the recommendation system.

### Function
# The recommendation system has three parts:
- Part 1: Access the New York Times API:
  * Use the query_url to include the page parameter.
  * Make a GET request to retrieve the page of results, and store the JSON data in a variable called reviews.
  * Add a 12-second interval between queries to stay within API query limits.
  * Write a try-except clause that performs the following actions:
  * try: loop through the reviews and append each review to the list, then print out the query page number (i.e. the number of times the loop has executed).
  * except: Print the page number that had no results then break from the loop.
  * Preview the first five results in JSON format using json.dumps with the argument indent=4 to format the data.
  * Convert reviews_list to a Pandas DataFrame using json_normalize()
  * Extract the movie title from the "headline.main" column and save it to a new column "title"by using the apply() method and the lambda function.
  * Use the supplied extract_keywords function to convert the "keywords" column from a list of dictionaries to strings using the apply() method.
  * Create a list called titles from the "title" column using to_list(). These titles will be used in the query for The Movie Database.
    
- Part 2: Access The Movie Database API:
  * Create an empty list called tmdb_movies_list to store the results from your API requests. This will contain a list of dictionaries.
  * Create a variable called request_counter and initialize it with the value of 1. This counter will do the following:
  * Increment by one every time you iterate through the titles list.
  * Use time.sleep(1) when it reaches a multiple of 50.
  * Print a message to indicate that the application is sleeping.
  * Loop through the titles list created from the movie reviews DataFrame, and perform the following actions:
  * Perform the actions outlined in Step 2.
  * Perform a GET request that sends the title to The Movie Database search and retrieves the JSON results.
  * Use a try clause that performs the following actions:
  * Collect the movie ID from the first result.
  * Make a GET request using the movie query and movie ID to retrieve the full movie details in JSON format.
  * Extract the genre names from the results into a list called genres.
  * Extract the spoken_languages' English name from the results into a list called spoken_languages.
  * Extract the production_countries' name from the results into a list called production_countries.
  * Create a dictionary with the following results: title, original_title, budget, original_language, homepage, overview, popularity, runtime, revenue, release_date, vote_average, vote_count, as well as the genres, spoken_languages, and production_countries lists you just created, and append this dictionary to tmdb_movies_list.
  * Print out the name of the movie and a message to indicate that the title was found.
  * Use the except clause to print out a statement if a movie is not found.
  * Preview the first five results in JSON format using json.dumps with the argument indent=4 to format the data.
  * Convert the results to a DataFrame called tmdb_df with pd.DataFrame().
- Part 3: Merge and Clean the Data for Export.
  * Merge the New York Times reviews and TMDB DataFrames on the title column.
  * The genres, spoken_languages, and production_countries columns were saved as lists, but we want the columns to be strings without the list characters ([, ], and '). To fix these columns, I performed the following actions:
  * Create a list of the columns that need fixing called columns_to_fix.
  * Create a list of characters to remove called characters_to_remove.
  * Loop through columns_to_fix and do the following:
  * Use astype() to convert the column to a string.
  * Loop through the characters_to_remove and use the Pandas str.replace() method to remove the character from the string.
  * Print the head of the updated DataFrame to confirm the list characters were removed.
  * Delete any duplicate rows and reset the index.
  * Export data to a CSV file without the DataFrame's index.

## Summary

This README provides a comprehensive approach to extracting, processing, and merging movie data for the recommendation system which includes detailed descriptions and parameters for each function, providing a clear roadmap for setting up and running the project.
