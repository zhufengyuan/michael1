# michael1
here is the project of practical machine learning
---
title: "Practical Machine Learning Project"
author: "zhufengyuan"
date: "Saturday, April 18, 2015"
output: html_document
---
Introduction

The goal of this analysis was to develop an accurate algorithm for predicting the manner of exercise being performed by 6 participants based on measurements collected from inexpensive personal activity sensors.

method

we download the data from website, and contain 19622 observations across 160 variables as training set, contain 20 observations across 160 variables as testing set. And use stratified sample extract the 11776 observations across 160 variables from training set to do this test.Leave the surplus section as the validation.

result

The out of bag error rate for the test is 86.07% accuracy. And the test result will be shown in table 1:

Table 1: Confusion matrix 
```{r}
##Reference |
##Prediction|  A  |  B  |  C  | D | E
##-| -----|----- |-----|-----|----
##A| 2142 | 63   | 11  |  2  |  0
##B|   62 | 1256 |  68 |  52 |   0
##C|   28 |  192 |1260 | 219 |  58
##D|    0 |    7 |  14 | 805 |  94
##E|    0 |    0 |  15 | 208 |1290
```
The rpart model performed similarly well on the validation dataset, predicting the outcome with 86.07% accuracy.

Conclusions

Many potential predictors were excluded from this analysis and additionally the final model was trained on only about 15% of the available data. Nonetheless a better accurate model was constructed using rpart(decision tree). The out of sample error from both the out-of-bag data and validation set are both less than 15%.

Going forward several more investigative analyses could be performed. For example this data could be further explored using a complete case analysis. An additional future analysis might be creating a random forest mehod using only the most important variables to see if model accuracy was similarly high. If so this would minimize the amount of data needed to be collected. And analysis might investigate building models that are better at distinguish certain levels of the outcome that are of particula interest. For the current model had the most trouble distinguising class D from class C (see Table 1), so if you are particularly interested in distinguishing between those outcomes tuning parameters could be tweaked to more finely tune your model.
