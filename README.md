# Movie Recommender System

This project implements three types of recommendation algorithms using the [MovieLens 100K dataset](https://grouplens.org/datasets/movielens/100k/):
- User-user collaborative filtering
- Item-item collaborative filtering
- Pixie-inspired random walk (unweighted and weighted)

These methods aim to suggest movies that a user might enjoy based on rating patterns or connections in a user–movie bipartite graph.

---

## Dataset

- Source: MovieLens 100K
- Size: 943 users, 1682 movies
- Ratings: Integer values from 1 to 5  
- Preprocessing:  
  - Merged user and movie metadata  
  - Pivoted into a user–movie ratings matrix  
  - Filled missing ratings with each user’s mean  
  - Normalized user ratings (z-score)

---

## Methods

### User-User Collaborative Filtering
- Computes cosine similarity between users based on normalized ratings  
- Predicts unrated movies using weighted averages from similar users  
- Recommends top-N movies with the highest predicted ratings

### Item-Item Collaborative Filtering
- Transposes the user-movie matrix  
- Computes cosine similarity between movies  
- Recommends similar movies to a given title

### Pixie-Inspired Random Walk
- Builds a bipartite graph between users and movie titles  
- Performs random walks to find frequently visited movies
- Two versions:
  - Unweighted: Uniform transition probability
  - Weighted: Biased by rating (acceptance probability proportional to rating)

---

## Examples

```python
# User-based recommendation
recommend_movies_for_user(user_id=1, num=10)

# Item-based recommendation
recommend_movies("Star Wars (1977)", num=10)

# Random walk recommendation
recommend_for_user(graph, user_id=1, walk_length=100000, top_n=10)

# Biased walk based on rating
recommend_similar_movies_biased_coin(graph_weight, "Star Wars (1977)", walk_length=100000, top_n=10)
