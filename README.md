# Ames-Housing-Price-Prediction

## Introduction

This project is a demonstration of the Data Science and Machine Learning skills I have developed from school and on the job learning.  The Ames Housing dataset was provided to me with little explanation about its background.  Upon further investigation I found it was developed as a modern replacement to the Boston Housing dataset for data scientists to practice their skills.  There is also an ongoing Kaggle Machine Learning competition using the dataset.   

In this analysis I plan to go through the standard Machine Learning process, exploratory data analysis, data cleaning, building models, and interpreting results to predict the selling price of a home.  Finally, I will address changes I would implement if circumstances were different.  

## Exploratory Data Analysis

The first thing that caught my attention was the size of the dataset.  With no cleaning there are 1,460 rows and 81 features.  Digging into the data we can see most features are categorical so if I want to include them in modeling I will need to convert them to dummies (one hot encode) thus increasing the number of features.  Because this is a regression problem adding unnecessary features can negatively affect the model’s predictability.  With this in mind I address the missing values.  

Most of the numeric features with missing values can be replaced by 0.  This is because if the data is missing based on related features the attribute is not present in the home.  However for the year the garage was built ('GarageYrBlt') we cannot replace this with 0.  I will test the model’s predictability withholding this feature.  I assume the categorical features follow the same pattern as the numeric features.  If the data is missing I replace the data with “Missing” or whatever the feature has to indicate the attribute is not present.  I elect to replace missing values where I can instead of removing these rows because the sample size is so small.  

Digging deeper into the data I look at the distribution of the features.  Here I look for two factors:  

1. Is there decent variation in the feature so the model can use that information to better predict price.
2. Are there outliers effecting the distribution. 


For the first case, there are a number of features I’d like to test the model’s predictability by holding them out. For the second, there is evidence to suggest outliers will effect model performance so I plan on normalizing the data.  Finally, continuing the effort to find features I can remove to improve model performance, I test correlations between the models features.  This resulted in expanding the list of feature to consider removing.  


## Data Cleaning

In addition to the basic data cleaning done in the Exploratory Data Analysis section I wanted to engineer a few new features with the hopes the new features could reduce the total feature count.  The features engineer can be broken into the following groups:  

1.	Age
2.	Bathrooms 
3.	Square Footage
4.	Outdoor Living (Deck & Porch Square Footage)
5.	Simplifying Categorical Features
For the last group, Simplifying Categorical Features, instead of have the all categorical descriptions of the attribute I wanted to convert them to whether the attribute is present or not.  Here I also normalize the data to control for outliers. To increase predictability I also filter the data to only “normal” sales conditions ("SaleCondition") and Residential homes (“MSZoning”).  


## Model Building

With the newly cleaned dataset I move on to building models.  As stated before, the goal of this project is to predict the selling price of a home, thus I will use regression algorithms.  The algorithms I use are listed below:  

1.	Linear Regression
2.	Random Forest
3.	Gradient Boosting
4.	Stochastic Gradient Descent
5.	Support Vector Machine


Using these algorithms, the features engineered, and the various test I’d like to run I construct a large loop to build models and estimate results.  The loop follows this pattern:  

1.	Get the features for the model
2.	Get the algorithm for building
3.	Prepare data for modeling
4.	Submit data to algorithms
5.	Gather model testing results

## Results

The best model turned out to be a Gradient Boosting model with a Mean Absolute Error (MAE) of $49,464.54.  This is alright when compared to the standard deviation of $79,442.50.  This model also had the most features removed.  

To understand how my testing went I developed an OLS regression to see how much my testing could explain the MAE.  This explanatory model’s R-Squared is 69.96%.  However, there are no variables that are statistically significant (P-Value < .05) so none of the attributes I was attempting to study had a significant impact on MAE.  


## Different Circumstances

Below I will list other things I would have tested to improve model performance.  

- Build unsupervised models for dimension reduction.  – This would be a continuation of the tests run above, however letting the machine find what works best. 
- Hyperparameter tune the models – In this analysis I took the algorithms off the self with their default hyperparameters.  If I had more computing power and time to train I would implement hypertuning methods.
- Convert the Sale Price it a discrete feature to then train classification models. – This would open up the analysis to more algorithms as well as evaluation criteria.  



