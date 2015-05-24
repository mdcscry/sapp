---
title       : Shiny App Sales Pitch 
subtitle    : Wide Receivers in the NFL combine
author      : Matthew Cryer
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Product Overview

The NFL is a 10 billion dollar business.  For many young athletes, this leads to outsized ambitions.  What does it take to make it to the NFL.  With a complete collection of NFL combine data and draft data from 1999 to present, this application will take three inputs and determine whether the athlete has the makings of a first or second round draft pick.  These picks make the lion's share of the money during early careers.  Young athletes are bombarded with the riches these picks command, yet have scant chance of acheiving that dream.  This product helps educate young athletes about their chances to make it to the big-time.

<img src='http://www.autisminvestigated.com/wp-content/uploads/2015/01/money.jpg'></img>

---.class #id

## The Model & Data
The data is pulled from two sites on the web.  It was process with complete automation.  No hand tailoring of the data was done.  This leads to some inaccuracy.  The two datasets from different sites have different names and spellings.  To normalize that a little, I stripped whitespace and punctuation.  Both sites used Caps for first letter of first and last.
The data was available from 1999-2015.  All data was downloaded and included in the model

Three models were tested.  randomForest(parRF), GBM and GLM were tested.
First attempts were to predict round of draft.  This was impossible.  I stepped back in complexity trying to determine where I could make distinction.  I tried multiple things settling on 1rst and 2nd round draft picks.  Accuracy really bloomed when I altered that to Third round, but that's not where the money is.

For the app, I rolled out the randomForest, but the GBM was just as good.  The main issue with the model is it has bad accuracy for actually predicting the 1rst and 2nd rounders.  It is very accurate at determining 3 round and later.

It is possible to say, if the model predicts 1rst and 2nd you have about a 50% chance of that happening.  If the model predicts later rounds or free agents its about 85% accurate.

---.class #id



```
## Loading required package: lattice
## Loading required package: ggplot2
## Loading required package: randomForest
## randomForest 4.6-10
## Type rfNews() to see new features/changes/bug fixes.
```

##### Method: parRF



```r
confusionMatrix(rf_predictions,testing$Round)
```

```
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction   0   1
##          0  18  27
##          1  40 141
##                                           
##                Accuracy : 0.7035          
##                  95% CI : (0.6394, 0.7623)
##     No Information Rate : 0.7434          
##     P-Value [Acc > NIR] : 0.9243          
##                                           
##                   Kappa : 0.1615          
##  Mcnemar's Test P-Value : 0.1426          
##                                           
##             Sensitivity : 0.31034         
##             Specificity : 0.83929         
##          Pos Pred Value : 0.40000         
##          Neg Pred Value : 0.77901         
##              Prevalence : 0.25664         
##          Detection Rate : 0.07965         
##    Detection Prevalence : 0.19912         
##       Balanced Accuracy : 0.57482         
##                                           
##        'Positive' Class : 0               
## 
```

---.class #id

## The Issues and Improvements

1. First rounders don't test.  Measures in all categories are required (looking at you Dez Bryant.)
2. Need to include college stats.
3. More Positions
4. More parameters
5. Model doesn't include colleges.





