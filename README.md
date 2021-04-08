# MovieLens Recommender System

#### Matthew Zhang, Adina Steinman

### Objective:
Our team of data scientists are working together for a new growing movie platform looking to compete with other giants such as Netflix, Hulu, and HBO. Our aim is to create a unique experience for each of our customers while subtly increasing company ROI. We aim to achieve this by building a tailored, unique recommendation system that can effectively suggest movies to our users, in order to continue to engage them with our platform. 

We want to be able to make predictions to our existing clients, as well as use our recommendation system as a product we use to attract new users to our platform. Additionally, as we continue to build up our recommendation systems, we plan to expand our platform by investing in newer and relevant content for users to enjoy.

<img src="https://github.com/adinas94/Phase4Project/blob/main/Images/Screen%20Shot%202021-01-28%20at%203.57.50%20PM.png" alt="alt text" width="600" height="400">

## Data
Our team used the “MovieLens” database, developed by the GroupLens research lab at the University of Minnesota.

The initial data set consisted of ~100,000 user ratings; then was reduced to ~47,000 once both users and movies with low number of ratings were removed to combat high matrix sparsity of around 99%.
Our final dataSet included information on userId, movieId, rating, title, genres and year.

## Goal
1. Use Collaborative Filtering to predict what users would rate movies that have not been seen before.
2. Demonstrate model predicability with Singular Value Decomposition (SVD)
3. Draw conclusions based on our data and model results.

<img src="https://github.com/adinas94/Phase4Project/blob/main/Images/Screen%20Shot%202021-01-28%20at%203.54.51%20PM.png" alt="alt text" width="350" height="400"> <img src="https://github.com/adinas94/Phase4Project/blob/main/Images/Screen%20Shot%202021-01-28%20at%203.55.29%20PM.png" alt="alt text" width="400" height="300">


### Exploratory Data Analysis and Post-Modeling
We wanted to emphasize the spread of movie ratings by looking at distributions and also how they would be visualized across each genre. 
To help understand this, we looked at a variety of different graphs using MatPlotLib to help get a better understanding of our data and to prepare for modeling.
Furthermore, we conducted post-modeling EDA to communicate the differences in ratings and how accurate our model performed.

Some observations/steps we had:
-Created genre labels in order to determine the most popular genres in the dataset; top 3 were Comedy, Drama, and Action  
-Analyzed the distribution of ratings: a rating of 4 was the most frequent 
-Analyzed the top 10 movies overall, as well as by genre, to use as a future comparison to post-model EDA to determine presence of popularity bias 

## Recommender Modeling
After thorough cleaning and exploratory data analysis, we began to run our recommender models. Beginning with a baseline SVD model. Without tuning any hyperparameters, the produced a root mean squared error (RMSE) of .80. We determined that on a rating scale of 0-5 that this performance was expected and was a good start. Moving forward, we explored other recommender algorithms within the Surprise library. In particular, we examined the performnace of models influcned by KNN or K-Nearest Neighbors that took a nearest neighbours approach based on similarity metrics. We tested KNNBasic, KNNWithMeans and KNNBaseline all performing the same or worse than our baseline SVD model; even after tuning.
To be precise, RMSE of KNNBasic=0.88, KNNWithMeans=0.81, KNNBaseline=0.80 and CV of KNNBasic=0.90, KNNWithMeans=0.82, KNNBaseline=0.82

<img src="https://github.com/adinas94/Phase4Project/blob/main/Images/Screen%20Shot%202021-01-28%20at%204.23.50%20PM.png" alt="alt text" width="300" height="200">

To help validate our models, we incorporated GridSearchCV while also running K-folds Cross Validation (3-folds). This helped us validate our model, but more importantly, efficiently tune the hyperparameters we fed in the model. Specifically, we determined that our model should be tuned by: the number of factors (n_factors=80), the regularization extent (reg_all=0.06), the number of epochs (n_epochs=30) and the learning rate of the model (lr_all=0.01).

FINAL Model: Our final was the tuned SVD model with an RMSE of 0.78 which is improved from our baseline and other model tests. This tells us that the model can estimate/predict ratings with an approximate error of 0.78 on a rating scale of 0-5.

#### Conclusions: 
Overall, our model does a fairly decent job of estimating users’ ratings, with an approximate error of 0.8
Our model is a purely collaborative filtering model, and therefore does not address the “cold start problem”

Our future work would: look to incorporate aspects of a content based filtering model to address this, specifically through the use of LightFm 
Incorporation of features, such as genres and year, into our matrix factorization models 

Finally, you can access the blog post that was inspired from this project by clicking here: https://adinasteinman.medium.com/building-a-collaborative-filtering-recommendation-system-in-surprise-91312f8cbbc6 
