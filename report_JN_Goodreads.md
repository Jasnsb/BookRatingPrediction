Project : Book rating prediction model.

By Jason NSIMBA (jason.nsimba@edu.dsti.institute).

## Resume
In this project, we worked with a dataset from Goodreads in order to set up an efficient prediction model for book rating. Before going on machine learning models which are future oriented, we decided to start with a short data analysis focused on the past and the present. Consequently, the project is subdivided in two parts : Data Analysis, and Prediction. 

## Part I : Data Analysis
First and foremost, we changed the original file because sometimes 2 authors or more contributed to a book, and all authors was separated by a comma, which is the separator between each field. We had to fix that otherwise an error occurred. 
During the first part, we look at the dataset to see if any cleaning was needed. This is the part “Overview of data”. We identified not any empty values. However, cleaning was necessary. Here, the list of all cleaning we made in “Data Cleaning” :
-	“num_page” : the header needed to be correct,
-	“isbn13” : needed to be convert from integer to string, 
-	“ratings_count” : Although some values were equal to 0, that wasn’t always the case for “average_ratings”. Therefore, we removed all lines with a “ratings_count” equal to 0,
-	“language_code”  : “en-CA”, “en-US”, “enm” corresponding respectively to Canadian English, United States English and Medium English, was processed to be “eng”,
-	“publication_date” : 2 dates hadn’t a valid format. 

Then in “Data Visualization”, we tried to answer to these 3 questions : 
- What’s the count of book per language ? 
- What’s the average rating per year ?
- What’s the top 3 highest rated publishers who have published at least 100 books ? 

We saw that books were unequally distributed regarding the language, with a huge domination by English (more than 10k) followed by Spanish (210) and French (140). For some, only one book is available (Aleut, Arabic … ). Despite some outliers, the average rating of a book is almost constant since 1900, with an average rating of 4. We also noticed that there were more books between 1960 and 2020 than before. The top 3 highest rated publishers are HarperCollins, Penguin Classics and Mariner Books. Nevertheless, the position of HarperCollins can be reconsidered because he published 112 books, when others published more than 150 books. Vintage is the most productive publisher, and almost the lowest rated. 

## Part II : Prediction
In order to have a sneak peek of the prediction part, we plotted the correlation matrix. The heatmap showed us poor correlations between the average rating and other quantitative variables. It is therefore difficult to believe that a prediction will be accurate, however we decided to go further for the sake of the exercise.
Firstly, we started with a classification way. In fact, the target is to predict whether a book will be good or not, thanks to some of its characteristics. Thus, we had to create groups, depending on the average ratings. Among other things, to have an accurate prediction, we need to do our best to have balanced groups. So after different classification models, (5 groups, 4 groups, 3 …) we set 2 categories : “Less good” and “Very Good” with respectively 55.39% and 44.61 % of representativeness in the dataset. “Very good” book are books with an average rating superior than 4. More groups would have been better of course, but with more than 2 groups we had disproportion between groups and that was not desirable. 

In “Features Engineering”, we dropped unusable columns to predict the group, such as title, authors, publisher ... They are unusable because they can’t be transformed into categories. We removed “month” and “day” too because their correlations with the average_rating were too weak. Books which are unique in their language were removed because with one example, a model can’t learn properly, it couldn’t be unbiased. Then, the language_code columns were binarized. 

In “Model selection and evaluation”, we chose and trained a Logistic Regression model. We hadn’t a good result enough, with a model which is able to predict a “Less good” book correctly (f1-score = 0.71), but not enough “Very good” one (f1-score : 0.32). The exercise aimed at predicting “Very good” books so obviously, this kind of outcome isn’t satisfactory.  We tried to improve our result in “Attempts to improve outcomes” through features engineering, dataset improvement (to increase the balance of groups, source : https://github.com/kart-projects/Goodreads-books) and even by testing other classic classification models (Decision Tree, Random Forest). Then we kept the best model in term of precision, recall and f1-score, which was the Random Forest with our enriched dataset using ratings_count, text_reviews count, num_pages, and language_code (Dataset splitting 4).
The classification model of the latter is exhibited below (figure 1)

![image](https://user-images.githubusercontent.com/94021364/171062170-b8e52dc4-cf13-4084-9be0-10cdc6f42b23.png)

We can see that the recall for the group “Very good” is inferior than the other. The recall is a metric which takes account of the type II errors (In this case, predict that a group will be “Less good” whereas it is “Very good”). For book prediction, we don’t have to care a lot about this error, because a misjudgment isn’t dramatic, nevertheless, better is the recall, better is the final result. The f1-score, which is the harmonic mean of the recall and the precision, is around 0.6 for each group. It means that 6 times per 10, the model predict correctly the group of a book. It’s not so bad, but it’s not enough to be really confident. Lastly, thanks to the work did earlier, we can see that the support is almost equal for both groups. This is a good point because it indicates that we have really a success ratio in estimation of group around 60%. 

Secondly, we tried a regression way. The goal is to predict an exact value of average rating, thanks to quantitative variables : ratings_count, text_reviews_count, num_pages. In “Model selection and evaluation”, we chose and trained a Linear Regression model. Results are outlined on figure 2a. Despite a weak Mean Absolute Error (0.22) and Maximum Residual Error (1.90), we can see that the Explained variance regression score and the coefficient of determination are very bad (both 0.04). The model is bad, but this is not a surprise. We can see on figure 2b that each variable doesn’t seem to be linearly correlated with the target variable. A non-linear regression could give a better result and can be a way to continue this work. 

![image](https://user-images.githubusercontent.com/94021364/171062309-9031693e-e029-4f16-b366-475f3cd61750.png)

## Conclusion : 
We can predict the group of a book with 60% of success, with a Random Forest model. To increase the success rate of the classifier, we can add more variables, more individuals. Linear models aren’t the best way to predict the average rating with current available variables.  To improve the result in a regression way, we can add variables (preferably more correlated to average rating), and try non-linear models. 
