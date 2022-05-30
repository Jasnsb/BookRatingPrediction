# Overview

Solving few business questions and training classification models (Logistic Regression, Decision Tree, Random Forest) to predict the category of a book based on its characteristics, and tried to improve outcomes. In a second part, we trained a Linear regression model to predict the exact value of the average rating. 

## Repository
Link to the project : https://github.com/Jasnsb/BookRatingPrediction/

## Description & way of thinking
A short report was build in order to highlight my way of thinking and my methodology to do this project. You can find it under the name "..."

## Data
Main data come from the Goodreads website (https://www.goodreads.com/). 
We had used additional data from https://github.com/kart-projects/Goodreads-books .

## Model
### Evaluation Data 
The split was done in 85:15 ratio (85% for training, 15% for testing). 

### Metrics 
To evaluate classification models, we used :
- Precision
- Recall
- F1 score

To evaluate the regression model, we used :
- Mean absolute error 
- Maximum residual error
- Explained variance regression score
- Coefficient of determination (R²) 

## Installation (local)

Install requirements 
- Activate a virtual environment (this version was tested on python 3.6)
- pip install -r requirements.txt
