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
