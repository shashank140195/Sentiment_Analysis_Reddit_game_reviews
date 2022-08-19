# Sentiment_Analysis_Reddit_game_reviews
Sentiment analysis of some of the game reviews posted on subreddit r/gaming. This project could help businesses to improve the areas where there users feel needs imrovement

This project contains the training file that we created from the game reviews on subrredit r/gaming. the training set was not readily avaialble and was 
mannualy created. Each comemnt has 5 facets for sentiment. We have classified sentiments into 3, Positive: if the user liked the feature, negatove: if the user didn't like the feature and neutral. 
if thet are not talking about the feature.
1. Controls: 
2. Graphics: 
3. Story:
4. Bugs:
5. Cost: 
 
Nearly more than 600 threads were extracted but many of them didn’t talk about the game reviews. Hence those comments were
filtered out. In the end, we were able to gather 400 comments. This data was downloaded into a CSV file using the python package pandas.

Labeling
Next, the data was labeled manually. Each comment was split into 5 categories:
overall sentiment towards the game, how good the controls were, how nice the graphics looked, how enjoyable
the story was, and how the sentiment towards the number of bugs in the game. The labels were then assigned
as either Positive, Neutral, or Negative for each facet. A positive sentiment means that the comment conveys
that the user is happy with that facet of the game. A neutral sentiment means that the comment does not
convey a positive or negative sentiment, or conveys both a positive and negative sentiment. A negative
sentiment means that the comment conveys that the user is unhappy or dissatisfied with that facet of the game.
An example of a positive overall sentiment comment with negative controls sentiment is “This game is amazing,
but the controls aren’t great.” This comment conveys that the user enjoyed the game overall, but displayed a
negative sentiment about the controls. For this project, 400 comments were labeled for each of the 5 facets for a
total of 2000 labels.

Methodology
data is pulled from Reddit, separated into multiple faceted datasets, and preprocessed. The data set is split into 75% training data and 25% 
testing data, then the training data sets are then run through count vectorization. The count vectorization is run
through a logistic regression model for training. The train test split data is used to pick the best N-gram range and
alpha value for each facet, and test these best choices against the test set. Finally, the models are deployed and
used to predict new review data and output the results.

Preprocessing
To improve the accuracy of the models, the dataset was put through multiple cleaning steps to remove
irrelevant data. First, all of the characters were converted to lowercase to create consistency in recognizing
words. This was done because of the informal nature of the data source, Reddit. Users may not write full
sentences, so capitalization can be misleading and is not a good tool for predicting sentiments. Additionally,
newline characters were replaced with spaces to improve consistency in the documentation. Finally, neutral
sentiments were removed from each set. Reviews with a neutral overall sentiment were removed before training
the overall sentiment model, reviews with a neutral controls sentiment were removed before training the
controls model, and this continued for each facet. Each time this parsing was done from the original dataset, so a
review with a neutral overall sentiment may still be used to train the controls model if it has a positive or negative controls sentiment

Classification
This project used logistic regression to develop the model for sentiment analysis. Specifically, the logistic
regression model from Scikit, using the LibLinear solver. Once the labels were converted to binary, the testing
sets were split into random training and validation sets and run using different alpha values to find the optimal
value for each facet model based on the alpha value with the highest average F1 score after 30 trials. These
alpha values were then used on the model fitted to the full training set for the respective facet then run on the
test data to get the F1 scores of each facet. Once the models were created, a wrapper function was created to
make a comment and predict a label for each facet. This would take in a review as the input, and output an
overall sentiment prediction, a controls prediction, a graphics prediction, a story prediction, and a bugs
prediction. This can be used for error analysis by determining why the model labels certain reviews differently by
running with different word choices and to get prediction labels for longer comments.

Part of Speech
The final step of this project was using Part-of-speech tagging (POS) to pull adjectives from positive and
negative prediction sets to find what adjectives are being used in these labels. Adjectives were chosen because
they are descriptive words, and are most likely to be useful to developers looking for specific feedback on their
games. For example, if users are commenting “beautiful” a lot, developers know that they should continue the
style of art currently in the game. To accomplish this, POS was run on the comment body for output. Next,
adjectives corresponding to positive labels were placed in a list, and adjectives corresponding to negative values
were put in a different list. These lists were then analyzed for the most frequently occurring words, which were
ranked and returned as the most frequently occurring adjectives for each list and their frequency.
