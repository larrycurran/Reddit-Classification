# Natural Language Processing - Classifying posts on two subreddits

### Executive Summary

The world needs the ability to distinguish between two similar, though otherwise distinct subreddits.  Subreddits are essentially online communities of interest where users post discussions, photos, videos, etc. The goal of this project is to create a model that best predicts where a post may come from given the language that is used.  This is a binary classification problem using Natural Language Processing and other classification models. 

The solution to this problem has real-world implications.  A model that can make these predictions can inform targeted marketing efforts for companies, and help reddit to sell their own ad space on the subreddits through outreach to companies that correlate to the language used.  

Through the analysis, the best model I came up with was through the use of Multinomial Naive Bayes.  This model had an accuracy score over 94% on the training data, and ~88% on the test data.  There were models that scored better on the training data, but those models were overfit.  
#### Choosing the subreddits

Choosing which subreddits was iteself a bit of a challenge, because I wanted to have topics that were similar enough to each other but also distinct.  Given the fact that hockey seson just started, as well as the recent successes of the Washington Nationals to get to the World series, I chose the /caps and /Nationals subreddits to analyze.  

---

### Obtaining and cleaning the data

I gathered the data using reddit's API, called PRAW.  PRAW allows the user to instantiate a reddit session and pull from a number of subreddits, including obtaining comments, photos, etc.  I used the get_top_from_year function to gain over 1500 posts from each subreddit, and I also made a grab of the current top posts on the subreddits.  I deleted the duplicate values and created dataframes for the nats and caps.  From this point, I noticed that without the ability to analyze photos, some of the body of the posts showed as blank.  To counter this, I used the title column and used feature engineering to created a column with the body and title together.  I then used regular expressions (RegEx) and other data cleaning methods to get each word on its own and ready for processing.  

### Modeling the data

I made several models.  First, I used count vectorization to create test and train dataframes of the text column.  Next, I used both pipeline and feature union to do two separate runs of multiple models.  For the first pipeline I used count vectorization and logistic regression, and I made ranges for the hyperparameters of the n_gram range, max features, and min/max_df.  This created a best score over 97%, but was very overfit. 

For the second iteration I used feature union to take the model to the next level.  Here I used both count vectorization and TFIDF, along with more hyperparameter ranges and adding stop words, to better fit the model.  This performed similarly to the first.

The last model I made used the CV dataframes to perform a multinomial naive bayes regression.  This scored lower on the training data, around 94%, but also got rid of some of the variance and scored around 88% on the test data.  Because of this, I considered it the best of the three models I made.  

---

### Results and Recommendations

The top words for each subreddit did not provide much insight in terms of marketing leads.  One recommendation I would make is to perhaps reach out to sports apparel companies to use the most discussed player names and put ads about merchandise for that player (or for the National's case, World Series gear).  This is intuitive, though, and would not require significant statistical modeling.

I would recommend for future research combining photo recognition models with the Natural Language Processing.  This would take a large amount of computing power, but could create the best model for this type of problem.

---

  
