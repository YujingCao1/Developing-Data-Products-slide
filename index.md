---
title       : Cell Body Segmentation Classifier
subtitle    : Developing Data Products Project
author      : Yujing Cao
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Background

Hill, LaPan, Li and Haney (2007) develop models to predict which cells in a high content screen were well segmented. The data consists of 119 imaging measurements on 2019. The original (segmentationOriginal) analysis used 1009 for training and 1010 as a test set. There are two different kinds of outcomes: Poorly Segmented (PS) and Well Segmented (WS).

The classifier which is created based on the dataset "segmentationOriginal" is used to predict which cells were well segmented. 

--- .class #id

## Theory
One machine learning method, regression tree, was applied to build the prediction model. The followings are steps were taken:
- Split the whole dataset into two sets: training set and testing set
- Use training set to build model with regression tree

```r
intrain=createDataPartition(segmentationOriginal$Case,list=FALSE)
training=subset(segmentationOriginal,Case=="Train")
testing=subset(segmentationOriginal,Case=="Test")
modelFit=train(Class~.,method="rpart",data=training)
```

--- .class #id

## Classification Tree
<img src="assets/fig/unnamed-chunk-2-1.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" width="700px" height="650px" style="display: block; margin: auto;" />

--- .class #id

## Conclusion

There are two decision nodes,"TotalIntenCh2" and "FiberWidthCh1", used to determine if cells were well segmented or not. Firstly, if TotalInteCh2 is less than 35000, then cells were poorly segmented, otherwise, go to check the value of FiberWidthCh1. If FiberWidthCh1 is less than 9.7, then cells were poorly segmented, otherwise, they were well segmented.




