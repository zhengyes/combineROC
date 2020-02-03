# combineROC
how to combine ROC curves in ggplot2

---
title: "combineROC"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

```{r, echo=FALSE}
#read data
om=read.csv("C:\\Users\\zs7hm\\Box Sync\\Zhengye Si\\Osteomyelitis\\Data\\ost.csv")
om=om[,-1]

#categorize
om[,c(2,3,4,6,7,8,9,10,16,17)] = apply(om[,c(2,3,4,6,7,8,9,10,16,17)], 2, factor)

#roc
library(pROC)
full.model=glm(om$Culture ~ . , data=om, family = binomial)
final.model=glm(om$Culture ~ om$BMI + om$surgery + om$WBC, family = binomial)
roc1=roc(om$Culture ,full.model$fitted.values)
roc2=roc(om$Culture ,final.model$fitted.values)
ggroc(list("first ROC" = roc1, "second ROC" = roc2),legacy.axes = T)

```
