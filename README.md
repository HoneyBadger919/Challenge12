# Challenge 12 Analysis Report

## Overview

In this analysis we want to compare the performance of two Logistic Regression algorithms, differing in the distribution of the examples they are trained on.
First we split the dataset in train and test and we proceed in two different ways: for the first one, we train our model with the data obtained from the splitting; while for the second one, we train our model on a resampled dataset, by means of the `RandomOverSampler` function, which allows us to increase the number of training examples belonging to the minor class to achieve a balanced dataset.

This analysis is conducted on a loan dataset, whose features are labeled in a binary classification way, which assess the loan goodness, hence categorizing the loans in: "bad" and "healthy".

After loading the dataset, by reviewing the labels, we can see that this is a imbalanced problem since, as it is usually in the financial world, healthy loans (label `0`) outnumber the bad ones (label `1`). In the notebook we can see the healthy loans are over 30 times more the bad ones.

### Analysis

First we start by splitting the dataset into training and testing examples, because later we'll use the training records to tune our models.
Since this is a binary classification problem we use the `LogisticRegression` function, which apply logistic regression to fit the data.
After instantiating the model we can train it by means of the `fit()` function on the training features. The function will require also the training labels relevant to the feature since this is a supervised learning algorithm, hence we need to tell in advance to the algorithm the right answer.
After tuning the model we can make predictions using the testing examples and compare the performance using the predicted values and the actual labels used as ground truth.

We can repeat the process for the second case, but here before training our model we need to resample the data. In this case we'll resample by means of oversampling, which is a technique that allows us to increase the number of records of the minor class in order to match the one of the bigger one. This is done by picking up elements of the minortiy class at random with replacement.
Once we have created a balanced dataset, it is possible to make prediction on this in the same manner as before.

## Results

* Machine Learning Model 1:
The overall accuracy, so the right prediction (positive or negative) divided by the sum of all predictions, scores 95% which may lead to think it is a good result. We can dissect more the information about the prediction by looking at the classification report which is the synthesis of the information contained in the confusion matrix.
From here we can see that the model does a very good job in terms of both precision and recall at predicting the `0` class, which is the major one; it scores almost 100% in precision and 99% in recall.
Anyhow the `1` class scores just 85% for precision and 90% for recall. We can see from the confusion matrix that we have 66 healthy predicted loans that turned out to be bad. This corresponds to roughly 10% of the total number of bad loans in our test set. We want to reduce this number since missing bad loans can lead us to poor financial decisions.

* Machine Learning Model 2:
For the Model trained with the balanced dataset we have an higher overall accuracy, scoring 99%.
The precision and recall for the `0` class stayed the same, while the class `1` improved in terms of recall and didn't change in terms of precision.
This improvement in recall means we're missing less bad loans in our prediction, just 5 from looking at the confusion matrix.
F1-score also improved from 0.85 to 0.92.

## Summary

From the evaluation of the results included above, we can state that the Model 2 is strongly suggested for an algorithmic implementation of a 'bad loan finder'. The precision for class 1 will be just 85%, meaning we're labeling more loans as bad which aren't, but these in the worst case will lead to more conservative financial decision making.
Moreover it presents a low number of missed bad loans (high recall).