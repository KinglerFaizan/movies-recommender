Of course. Here is a comprehensive `README.md` file based on the provided Jupyter Notebook. You can copy the content below and save it in a file named `README.md`.

-----

# Movie Recommendation System

## Overview

This project is a content-based movie recommendation system built in Python. It suggests movies to users based on the content and attributes of a movie they like, such as its genre, director, main cast, and plot summary. The system processes a dataset of over 4,800 movies, creates a feature vector for each, and then recommends movies that are most similar in that vector space.

## Features

  - Merges and cleans data from multiple sources.
  - Engineers a unified text-based feature set for each movie.
  - Utilizes Natural Language Processing (NLP) for text normalization.
  - Builds a content-based filtering model using cosine similarity.
  - Provides a list of top movie recommendations for a given movie title.

## Dataset

The project uses the "TMDB 5000 Movie Dataset" which consists of two CSV files:

  - [cite\_start]`tmdb_5000_movies.csv`: Contains detailed information about the movies[cite: 2].
  - [cite\_start]`tmdb_5000_credits.csv`: Contains cast and crew information for each movie[cite: 2].

## Workflow & Methodology

1.  **Data Loading and Merging**:

      - [cite\_start]The two datasets (`movies` and `credits`) are loaded into pandas DataFrames[cite: 2].
      - [cite\_start]The DataFrames are merged into a single DataFrame based on the movie 'title'[cite: 5]. The resulting dataset has 4809 rows and 23 columns.

2.  **Data Cleaning and Feature Selection**:

      - [cite\_start]Irrelevant columns are dropped, and only essential features are kept: `id`, `title`, `genres`, `cast`, `crew`, and `overview`[cite: 9].
      - [cite\_start]Rows with missing `overview` data are dropped to ensure data quality[cite: 10, 11].

3.  **Feature Engineering & Preprocessing**:

      - [cite\_start]Helper functions are used to parse the JSON-like string data in `genres`, `cast`, and `crew` columns to extract relevant information[cite: 14, 17, 20]:
          - [cite\_start]All genre names are extracted for each movie[cite: 15].
          - [cite\_start]The names of the top 3 cast members are extracted[cite: 18].
          - [cite\_start]The director's name is extracted from the crew data[cite: 21].
      - [cite\_start]Spaces are removed from names (e.g., "Sam Worthington" becomes "SamWorthington") to treat them as single entities[cite: 26, 27].
      - [cite\_start]A new feature column named `tags` is created by combining the preprocessed `overview`, `genres`, `cast`, and `crew` columns[cite: 28].

4.  **Text Vectorization (NLP)**:

      - [cite\_start]The `tags` column is converted to lowercase for consistency[cite: 32].
      - [cite\_start]**Stemming** is applied to the text using NLTK's `PorterStemmer` to reduce words to their root form (e.g., "actions" becomes "action")[cite: 34, 35, 40].
      - The text data is converted into a numerical format using `CountVectorizer` from Scikit-Learn. [cite\_start]This process creates a vocabulary of the top **5,000** most frequent words (features) and removes English stop words[cite: 37].
      - [cite\_start]This results in a matrix of vectors with a shape of (4809, 5000), where each row is a movie and each column is a word from the vocabulary[cite: 38].

5.  **Model Building**:

      - [cite\_start]The **cosine similarity** metric is used to calculate the similarity between every pair of movie vectors[cite: 41, 42]. [cite\_start]This creates a 4809x4809 similarity matrix where each value represents the similarity score between two movies[cite: 42].

6.  **Recommendation Function**:

      - [cite\_start]A function `recommend(movie)` is defined that takes a movie title as input[cite: 46].
      - [cite\_start]It finds the index of the input movie and retrieves its similarity vector from the similarity matrix[cite: 46].
      - [cite\_start]It sorts the similarity scores in descending order and returns the titles of the top 7 most similar movies[cite: 46, 47].

7.  **Exporting the Model**:

      - [cite\_start]The final DataFrame containing the movie titles and tags is saved as a dictionary to a `.pkl` file using `pickle` for use in deployment[cite: 48, 49].

## Technologies Used

  - **Python**
  - [cite\_start]**Pandas**: For data manipulation and analysis[cite: 1].
  - [cite\_start]**NumPy**: For numerical operations[cite: 1].
  - [cite\_start]**NLTK (Natural Language Toolkit)**: For stemming and other NLP tasks[cite: 33, 34].
  - [cite\_start]**Scikit-learn**: For `CountVectorizer` and `cosine_similarity`[cite: 36, 41].
  - [cite\_start]**Pickle**: For saving the processed data and model[cite: 48].
  - **Jupyter Notebook**: For development and experimentation.

## How to Run the Project

1.  **Prerequisites**:

      - Ensure you have Python 3 installed.
      - Install the required libraries:
        ```bash
        pip install numpy pandas nltk scikit-learn
        ```

2.  **Dataset**:

      - Download the `tmdb_5000_movies.csv` and `tmdb_5000_credits.csv` files and place them in the same directory as the notebook.

3.  **Execution**:

      - Open and run the Jupyter Notebook (`Untitled.ipynb`) from top to bottom.
      - The notebook will perform all preprocessing steps and create the recommendation model.
      - You can use the `recommend('Movie Name')` function in the final cells to get recommendations.

## Example Output

Here is an example of calling the recommendation function for the movie 'Avatar':

```python
recommend('Avatar')
```

**Output:**

```
The Helix... Loaded
Small Soldiers
Godzilla 2000
Journey 2: The Mysterious Island
Beowulf
Mad Max Beyond Thunderdome
Apollo 18
```

[cite\_start][cite: 47]
