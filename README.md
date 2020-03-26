# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Web APIs & NLP

### Table of Contents:

- [Problem Statement](#Problem-Statement)
- [Executive Summary](#Executive-Summary)
- [Conclusions and Recommendations](#Conclusions-and-Recommendations)
- [Sources](#Sources)

---
### Problem Statement

Reddit is an American social news aggregation, web content rating, and discussion website based off the definition on [Google](https://www.google.com/search?q=reddit&rlz=1C5CHFA_enUS877US877&oq=reddit+&aqs=chrome.0.69i59j35i39j0l2j69i60l4.4152j0j7&sourceid=chrome&ie=UTF-8). Suggested from the [Reddit's website](https://www.redditinc.com/), it has over 130,000 communities that are in the form of "subreddits". Each page is a platform where the Users can post, comment, and vote. A "post" is where the community share content by stories, links, images, and videos. A "comment" provides discussions on posts. And both comments & posts can be scored by being upvoted or downvoted. Yet, there is a dilemma, what if we wanted to gather data and model mulitple "subreddits"? This is difficult to compare such information without a classifier. Thus, **can we use supervised machine learning to classify similar content from two different web sources?**

*How do we investigate this problem?* We scraped about 1000 posts from two chosen subreddits. Each subreddit we scraped was about 500 posts by using Reddit's API. Then, we finally used natural language processing to train a classifier model to check which post came for the correct subreddit. The classification models we decided to use were Logistic Regression, Bernoulli Naive Bayes, Bagged Decision Tree, and Random Forest which we evaluated on accuracy scores and results from confusion matrices. 

---

### Executive Summary

We begin by pulling the data from the two subreddits by using Reddit's API. The subreddits that we pulled were the r/Books and r/Movies subreddits. The data that was imported was in JSON format. Therefore, we decided to create dataframes in Pandas to have easier access to clean and manipulate through the data.

Once, we looked through the dataframes, we looked for particular subfields using the Reddit's API data dictionary. We focused on the title, author, selftext, and subreddit features. We chose these as the subfields because we wanted the best features for our modeling. 

Next, we did some data cleaning. We checked for duplicate posts and missing values in each of the dataframes. 

Then, we did some exploratory data analysis. We checked for the summary statistics and as a result, we dropped the selftext feature. Thinking back on our problem statement, we want to detemine similar content in both of the datasets, thus, we do this by looking at the frequently occurring words in each dataframe. We will did this by using an NLP functions called stemming and countvectorizer. We then chose to display bar graphs that had the top 20 frequently occurring single gram word & bigram words in each subreddit. Finally, we determined the outliers in each of our dataframes. 

Next, we were able to preprocess. We merged our datasets into one and dropped the author feature because we do not need it for modeling. We mapped our target variable: subreddit into a binary classification. We did some more NLP processing. We used lemmatization, stemming, and stopwords to analyize our dataset futher. Then, we created our X feature and target variable and did a train-test split. We decided to change our X feature as a stem version for our modeling. Lastly, we determined the basline score to compare to our models' results.

Finally, we were able to model. We modeled four different classification models. We modeled Logistic Regression, Bernoulli Naive Bayes, Bagged Decision Tree, and Random Forest. We also created a confusion matrix for each model to have further insights on each of our models. We wanted to see how well our models were able to correctly classify where each post came from. In the end, we focused on accuracy score and the bias-variance tradeoff from each  model to determined which model was the best to answer our problem statement.

---

### Conclusions and Recommendations

|Model|Training Accuracy Score|Testing Accuracy Score|Correctly Classified|Misclassified|
|---|---|---|---|---|
|Logistic Regression|0.997|0.816|257 posts|58 posts|
|Bernoulli Naive Bayes|0.973|0.835|257 posts|58 posts|
|Bagged Decision Tree|0.991|0.759|239 posts|76 posts|
|Random forest|0.998|0.778|245 posts|70 posts|


All the classification models: Logistic Regression, Bernoulli Naive Bayes, Bagged Decision Tree, and Random Forest surpassed the baseline accuracy. Yet, the **Bernoulli Naive Bayes Classification Model** was the best model to test our training data because it was able to manage well with unknown data according to the testing accuracy score.

However, the model was still overfit because of low bias and high variance.

Despite the overfitting, this model was able to classified similar content from two different web sources: r/books and r/movies. Also it was able to identify where each post came from which subreddit. It had one of the highest in correctly classifying posts which was 257. Therefore, Reddit will be able to implement this model for their studies on this data science topic. 

Yet, this model still had its limitations. Some of the posts had similar titles and incorrect spelling. It was not able to identify these mishaps because of NLP transformer. In other words, both of these mishaps could of swayed our model results. 

Also, our model can improve it's accuracy if we further tuned our hyperparameters. Additionally, we could of instantiate the PolynomialFeatures before our model to decrease the overfitting.

So we still have some recommend questions we need to ask:

- Should we increase the stopword list with more nouns to have a better predictable model? (i.e. ‘like’ and ‘help’)
- Each of the subreddits change over time, so will our model still predict accurately?  
- More specifically when big blockbuster movies come out, i.e. Superhero films, will our model still accurately predict given r/books does not talk about comics?  
- Will a different model that we had not yet modeled produce a better accuracy score? (i.e. SLM, Adaboost)
---

### Sources

“Reddit.” Google, https://www.google.com/search?q=reddit&rlz=1C5CHFA_enUS877US877&oq=reddit+&aqs=chrome.0.69i59j35i39j0l2j69i60l4.4152j0j7&sourceid=chrome&ie=UTF-8. Accessed 28 January 2020. 

“Reddit Homepage.” Reddit, https://www.redditinc.com/. Accessed 28 January 2020. 

“r/Books Homepage.” Reddit, https://www.reddit.com/r/books/. Accessed 29 January 2020.

“r/Movies Homepage.” Reddit, https://www.reddit.com/r/movies/. Accessed 29 January 2020.

“Pushshift Reddit API Documentation.” GitHub, https://github.com/pushshift/api. Accessed 24 January 2020.

“Options and settings Overview” Pandas, https://pandas.pydata.org/pandas-docs/stable/user_guide/options.html Accessed 29 January 2020.

“Stopword removal with NLTK and Pandas.” Stackoverflow, https://stackoverflow.com/questions/33245567/stopword-removal-with-nltk-and-pandas. Accessed 28 January 2020. 
