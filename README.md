**1.INTRODUCTION**

**Bussiness Understanding**

In the competitive landscape of streaming services,with numerous online platforms offering vast libraries of content, a *personalized User Experience* is crucial to deliver a tailored movie-watching experience which encourages longer viewing times, reduces churn rates and improves user satisfaction fostering a deeper connection between the user and the platform 

**Problem statement**

With the increasing volume of movies available across various platforms, users often face difficulty in discovering movies that align with their preferences. Moreover, understanding patterns in user behavior and movie trends is crucial for optimizing recommendation algorithms. The goal is to develop an effective recommendation system and gain insights into user preferences and movie popularity, thereby enhancing user engagement and satisfaction.The system should cater to diverse user preferences and handle the cold start problem for new users with limited rating history.

**Project Objectives**
* To perform data cleaning and exploratory data analysis (EDA) on a movie dataset, which includes user ratings, movie metadata, and tags.
* To build and evaluate different filtering recommendation algorithms, including:
     - **User-based collaborative filtering**
     - **Item-based collaborative filtering**
     - **Model-based collaborative filtering**
     - **Content-based filtering**
* To compare the performance of these algorithms and identify the most effective approach for movie recommendations.
* Implement a hybrid approach that combines collaborative and content-based filtering to address the cold start problem.
* Evaluate the performance of the recommendation model using metrics like RMSE, MAE.
* Provide actionable insights based on user preferences and feedback for continuous improvement of the recommendation system.

**Limitations**


*Limitations*

* **Cold Start Problem:**
New users with few or no ratings may not receive optimal recommendations due to insufficient data for accurate predictions.
* **Data Sparsity:**
The user-item matrix can be sparse, leading to challenges in finding similar users or items, which can affect recommendation accuracy.
* **Static Dataset:**
The MovieLens dataset may not reflect current trends, preferences, or newly released movies, limiting the system's ability to recommend the latest content.
* **Scalability:**
The collaborative filtering approach may face performance issues as the user base and item catalog grow, potentially slowing down recommendation generation.
* **Subjectivity of Ratings:**
User ratings are subjective and can vary widely; different users may interpret the rating scale differently, leading to inconsistencies in the dataset.
* **Limited Contextual Awareness:**
The system may not consider contextual factors (e.g., time of day, user mood, or social influences) that can affect movie preferences.
* **Implementation Complexity:**
While the hybrid approach can improve recommendations, it adds complexity to the system, requiring careful tuning and integration of multiple algorithms

**2.DATA**

This dataset (ml-latest-small) describes 5-star rating and free-text tagging activity from MovieLens, a movie recommendation service. It contains 100836 ratings and 3683 tag applications across 9742 movies. These data were created by 610 users between March 29, 1996 and September 24, 2018. This dataset was generated on September 26, 2018.

Users were selected at random for inclusion. All selected users had rated at least 20 movies. No demographic information is included. Each user is represented

**2.1 Data Understanding and Exploratory Data Analysis (EDA)**

Import the DataFiles
![image](https://github.com/user-attachments/assets/dfa466f4-f07f-4424-85f6-dbac3442e762)
**Summary Of Key Insights Of The 'movies' Dataset**

* The Dataset contains information about 9742 *links*, including their *movieIDs* and websites the were sorced from *imbdid* and *tmdbid* (3 columns) and there data types.
* The dataset has 8 missing entries from the *tmdbid* .No duplicate values

* ![image](https://github.com/user-attachments/assets/e84d3a40-ef68-415f-8371-0e7749d1dda3)

* **Summary Of Key Insights Of The 'movies' Dataset**

* The Dataset contains information about 9742 *movies*(Rows), including their *movieIDs*, *titles* and *genres* (3 columns) and there data types.
* The dataset has no missing or duplicate values

![image](https://github.com/user-attachments/assets/538018bf-025d-4b46-ac4b-24acffa11355)
**Summary of key insights of the 'ratigs' Dataset**

* The Dataset contains information about 100836 user *ratings* (Rows), including *userIds*,*movieId*(Foreign key) rating and *timestamp* indicating when the rating was made(4 columns) and their data types
* The dataset has no missing or duplicate values
![image](https://github.com/user-attachments/assets/e5e84a51-cb4b-4c8d-ad22-67d265978583)

**Summary of key insights of the 'tags' Dataset**

* The Dataset contains information about 3683 *tags* assigned by the user (Rows), including *userIds*,*movieId*(Foreign keys) *tags* and *timestamp* indicating when the tags were added(4 columns) and their data types
* The dataset has no missing or duplicate values

* 

We begin with timestamp conversion on ratings and tags dataframes to convert into a readable format by creating a fuction that we can fit both dataframes.
![image](https://github.com/user-attachments/assets/230fb501-0518-4bac-801d-909be78aab75)

![image](https://github.com/user-attachments/assets/1f703fd2-8380-4f1e-940b-4c98e1c73ea9)


* Next we Explode the movie_df to avoid the problem of sparcity.
![image](https://github.com/user-attachments/assets/10e9874b-795e-4728-934d-18ae7d483929)
![image](https://github.com/user-attachments/assets/30e04063-5866-46ec-b568-0886cb4a1bef)

Merge our movies and ratings dataframes since they have the components we need for the recomendation system we are to create.
![image](https://github.com/user-attachments/assets/a391c932-b0ab-4290-afc1-534aa31d4876)

**2.2 Data Analysis**

**2.2.1 Distribution of Ratings**

We begin by visualizing the ratings distribution to see how users have rated the movies.
![image](https://github.com/user-attachments/assets/27e862e6-37a2-456a-a6ac-bd72410eef72)
* The ratings are highly concentrated around 4, with a peak between 3.5 and 4. This suggests that users generally tend to rate movies favorably, with 4 being the most frequent rating.   

*There is a clear tendency for users to give high ratings (between 3 and 5). Low ratings (below 2) are much less frequent, indicating that most movies are either liked or considered average by the users. 


**2.2.2 Popular Genres**   

To analyze the popular genres, we'll extract individual genres from the df_movies dataset and count the occurrences.
![image](https://github.com/user-attachments/assets/530d3549-eaeb-4acd-b0b1-068e4b750b80)
`Drama` and `Comedy` are by far the most popular genres, with both appearing in over 4000 movies.     
`Thriller`, `Action`, and `Romance` are also popular, though with slightly fewer appearances.   
Genres like `War`, `Musical`, `Western`, and `IMAX` are much less frequent.  
There's a small portion of movies where no genres are listed, which might be worth investigating.

**2.2.3 Average  Rating By Genres**
![image](https://github.com/user-attachments/assets/6e7a828b-e377-4038-9f2d-79eb2bc9cf45)

The ratings are quite consistent across genres, with all averaging between approximately 3.0 and 4.0. Film Noir has the highest average rating, slightly above 3.8, while Horror has the lowest, just below 3.2. This suggests that, on average, viewers tend to rate movies in genres like Film Noir, War, and Documentary slightly higher, while Horror movies tend to receive relatively lower ratings

**2.2.4 Distribution of Rating Count by user**
![image](https://github.com/user-attachments/assets/9f2a7872-ad6f-4ba2-ae9b-549358b0e419)


This visualization tracks how user ratings change with count. 
It's helpful for spotting trends, such as whether ratings how willing the users are willing to rate and ot is clear that most users don't raising a concern for sparcity in our data.

**2.2.5 Time-based Analysis of Ratings**

This visualization tracks how user ratings change over time.

It's helpful for spotting trends, such as whether ratings for certain movies or genres are rising or falling in popularity.

We convert the timestamp into a year and then calculate the average rating per year.
A line plot is used here to track the evolution of average ratings over time.
![image](https://github.com/user-attachments/assets/b7b49955-f928-4551-a4e3-5e610ca96785)


**3.PREPROCESSING AND MODELING**

 **Recommendation Systems Algorithms:-**

 - 3.1KNN algorithm

*a. User-based collaborative filtering*
* Eradicate sparcity problem by increasing our data density.
![image](https://github.com/user-attachments/assets/cbde2ab8-bcc9-4c5e-9501-14f6cb0f8f52)
* Create user-item matrix.
![image](https://github.com/user-attachments/assets/5942edba-51d4-4d0d-bdea-441f89c219ad)
* Train-test split
![image](https://github.com/user-attachments/assets/23f0ce00-3a18-4584-a559-f3e5d17db525)
* Define a pipeline for the knn model.
![image](https://github.com/user-attachments/assets/ab2700db-4c78-4223-9f3c-82782e942c53)
* Model Evaluation
![image](https://github.com/user-attachments/assets/d96b9aaa-2d08-417c-9be1-d740b8059bc4)



*b. Item-based collaborative filtering*
![image](https://github.com/user-attachments/assets/7321081c-02de-4f5f-a585-d78a56384e02)
* Model evaluation
* ![image](https://github.com/user-attachments/assets/2d2ced04-0a8c-48f5-a171-30c9e87abfe7)

- 3.2 Model-based algorithm
 ![image](https://github.com/user-attachments/assets/f1e0590b-ba15-4ae8-8eb9-15dd868d15bf)
  
- 3.3 Content based algorithm
 ![image](https://github.com/user-attachments/assets/9f41cc11-13bd-4783-b279-eac9b82d443b)

- 3.4 Hybrid algorithm
![image](https://github.com/user-attachments/assets/24cd41e3-9ae8-4db2-9b7b-2f64dc1ee47e)


### 4. Project Findings
   - **Exploratory Data Analysis (EDA):** The dataset requires timestamp conversion. Ratings data reveals a distribution skewed towards higher ratings, with 4 and 5-star ratings being the most common. 
   - **Genre Distribution:** Some genres are more popular than others, with Drama, Comedy, and Thriller being among the top genres.
   - **Collaborative Filtering (User and Item-Based):** Collaborative filtering based on users and items provides recommendations based on similar users or movies. Both user-based and item-based collaborative filtering were implemented using k-nearest neighbors (KNN) and evaluated using metrics such as RMSE and MAE.
   - **Model-Based Collaborative Filtering:** Using Singular Value Decomposition (SVD), the system predicts ratings for unrated movies based on learned patterns in the ratings matrix. The SVD model yielded relatively low RMSE, indicating strong predictive performance.
   - **Content-Based Filtering:** By utilizing TF-IDF vectors of genres, this approach successfully recommended movies with similar genres to the target movie.
   - **Hybrid Recommendation System:** Combining collaborative filtering and content-based filtering with weighted scores resulted in a comprehensive approach that capitalizes on the strengths of both methods.
   - **Performance Metrics:** The RMSE and MAE metrics indicate that the model-based (SVD) and hybrid approaches provide a balance between accuracy and computational efficiency.

  ### Conclusions
   The project demonstrates the effectiveness of various recommendation systems. Collaborative filtering works well when user and item interactions are dense, but may struggle with sparse datasets. Model-based filtering (SVD) offers a good balance of accuracy and scalability, while the hybrid system enhances recommendation quality by combining collaborative and content-based approaches.

   ###  Recommendations

 - For production, implement a hybrid model with a tunable weight between collaborative and content-based scores to personalize recommendations further based on user behavior.This helps address the "cold start" problem for new users or movies with few ratings.
 -  Implement strategies to account for user biases in ratings, such as users who consistently rate movies higher or lower than average. Normalizing ratings or weighing ratings based on user behavior can improve recommendation
- Regularly update the recommendation system with new ratings and movie data to keep the recommendations relevant.
- Monitor the system performance over time and retrain models periodically to maintain high accuracy as user preferences evolve.
- Consider expanding the model to include additional features (e.g., movie descriptions, directors, actors) to improve the content-based component and enhance recommendation diversity.
