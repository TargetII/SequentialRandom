---
title: "SequatialRandom"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Sequantial random.  Just getting random sequence first.  First set the completely random generator.  Then generate a sequence
```{r}
N = 10
parms = crPar(N)
rs = genSeq(parms)
rsList = getRandList(rs)
rsList = t(rsList); rsList
write.csv(rsList, "rsList.csv", row.names = FALSE)
```
Try block rand first.  Ok this makes sense.  We figure out which groups we want to stratify or block on then it generates a random sequences for that group based on the number of people we want to randomize.  Still not sure why we need the block sizes, I think it is to help ensure that not too many people get assigned to treatment and or control.  

If you have three strats, then you need to include the intersection of each, because they could be in multiple categories.  For example, if you have female, male, low, and high risk then you also need groups for male low, male high, female low, female high to make sure there is not overlap. You have to be either male or female or low and high so have the intersections works.     
```{r}
library(blockrand)

male = blockrand(n = 100, id.prefix = "M", block.prefix = "M", stratum = "Male")
male
female = blockrand(n = 100, id.prefix = "F", stratum = "Female")

my.study = rbind(male, female); my.study
```
Trying big stick design
```{r}
library(randomizeR)
bigStickDesign = bsdPar(100, 2, groups = c("Treatment", "Control"))

bsdRand(N = 100, mti = 2, K = 2)
genSeq(bigStickDesign, r = 10)
```


