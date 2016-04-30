---
title       : Application caculates RMSE of the duration of the eruption for the Old Faithful geyser
subtitle    : 
author      : Thuyen Ho
job         : Web developer
framework   : html5slides      # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Agenda

1. Summary dataset
2. Create training and testing sets
3. Build and summary a model fit
4. Calculate RMSE on training and testing sets

---

## Summary dataset

- Load dataset


```r
  data(faithful)
```

- Summary dataset


```r
  summary(faithful)
```

```
##    eruptions        waiting    
##  Min.   :1.600   Min.   :43.0  
##  1st Qu.:2.163   1st Qu.:58.0  
##  Median :4.000   Median :76.0  
##  Mean   :3.488   Mean   :70.9  
##  3rd Qu.:4.454   3rd Qu.:82.0  
##  Max.   :5.100   Max.   :96.0
```

---

## Create training and testing sets

Create training set with 70% percent of dataset




```r
inTrain <- createDataPartition(y=faithful$waiting, p=0.5, list=FALSE)
trainFaith <- faithful[inTrain,]; testFaith <- faithful[-inTrain,]
```

---

## Build and summary a model fit


```r
lm1 <- lm(eruptions ~ waiting,data=trainFaith)
summary(lm1)
```

```
## 
## Call:
## lm(formula = eruptions ~ waiting, data = trainFaith)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -1.30114 -0.37501  0.06992  0.36080  0.96442 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept) -1.787883   0.224832  -7.952 6.54e-13 ***
## waiting      0.074313   0.003129  23.750  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 0.5079 on 135 degrees of freedom
## Multiple R-squared:  0.8069,	Adjusted R-squared:  0.8055 
## F-statistic: 564.1 on 1 and 135 DF,  p-value: < 2.2e-16
```

---

## Calculate RMSE on training and testing sets


```r
c(trainRMSE = sqrt(sum((lm1$fitted-trainFaith$eruptions)^2)),
    testRMSE = sqrt(sum((predict(lm1,newdata=testFaith)-testFaith$eruptions)^2)))
```

```
## trainRMSE  testRMSE 
##  5.901501  5.642199
```
