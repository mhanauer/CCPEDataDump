---
title: "CCPEDDataDump"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```


INSTRMNT_LANG	=1	
GRANT_ID = 	SP021203 # just do this manually
DESIGNGRP = 1
PARTID	
MONTH	DAY	YEAR	
INTTYPE =3	
INTDUR = 3

First step is to make sure that the Redcap people all have the required values.
Next step is to figure out how to get the date.
Final step is put the data set back together again.

```{r}

test = gpraAdult3month
dim(test)
# split data for those in redcap
n = dim(test)[1]
test = test[83:n,]
dim(test)
n = dim(test)[1]
test$INSTRMNT_LANG = rep(1, n)

test$DESIGNGRP = rep(1, n)
test$INTTYPE = rep(3, n)
test$INTDUR = rep(3,n)

```
I think I need to merge just the timestamp with 3month GRPA.  Need to grab the partID for both the merge on the ID.  That should get the time stamp.
First need to grab the time stamp before you delete it.  

```{r}
#gpraAdultBase = read.spss("S:/Indiana Research & Evaluation/CCPE/CCPE SPSS - Datasets/Baseline Adult/CCPE GRPA - Baseline.sav", use.value.labels = FALSE, to.data.frame = TRUE)
gpraAdult3month = read.spss("S:/Indiana Research & Evaluation/CCPE/CCPE SPSS - Datasets/3 Month Reassessments ADULT/Reassess 3M CCPE GPRA Adult.sav", use.value.labels = FALSE, to.data.frame = TRUE)
## Need to add the 3 month from the Red for the only GRPA and all assessments, but just drop all other assessments so everything after svytruth
setwd("S:/Indiana Research & Evaluation/CCPE/CCPE SPSS - Datasets/3 Month Reassessments ADULT")
gpraAdult3monthRedCap = read.csv("CCPEFollowupAdultQueRedCap.csv", header = TRUE)
gpraAdult3monthRedCapFull = read.csv("CCPEFollowupAdultQueRedCapFull.csv", header = TRUE)
# Need to get rid of extra for red cap full

gpraAdult3monthRedCapFull = gpraAdult3monthRedCapFull[,1:145]
gpraAdult3monthRedCap = gpraAdult3monthRedCap[,1:145]
gpraAdult3monthRedCapAll = rbind(gpraAdult3monthRedCapFull, gpraAdult3monthRedCap)
# Missing several variables and id value not the same
# First make the variables all upper case

names(gpraAdult3monthRedCapAll) = toupper(names(gpraAdult3monthRedCapAll))
# These don't match RECORD_ID REDCAP_SURVEY_IDENTIFIER NATIONAL_MINORITY_SAHIV_PREVENTION_INITIATIVE_ADUL_TIMESTAMP                 NAME
head(gpraAdult3monthRedCapAll)
#Subset only those REDCAP_SURVEY_IDENTIFIER with none na's
gpraAdult3monthRedCapAll = subset(gpraAdult3monthRedCapAll, REDCAP_SURVEY_IDENTIFIER > 0)
# Need to change these to just a year.
gpraAdult3monthRedCapAll$NATIONAL_MINORITY_SAHIV_PREVENTION_INITIATIVE_ADUL_TIMESTAMP
YEAR = data.frame(gpraAdult3monthRedCapAll$NATIONAL_MINORITY_SAHIV_PREVENTION_INITIATIVE_ADUL_TIMESTAMP)
colnames(YEAR) = c("YEAR")

YEAR = data.frame(apply(YEAR, 2, function(x){ifelse(x > 12/13/2016, 2017, ifelse(x > 12/31/2017, 2018, x))}))
# Need to get rid of RECORD_ID, NATIONAL_MINORITY_SAHIV_PREVENTION_INITIATIVE_ADUL_TIMESTAMP, NAME
gpraAdult3monthRedCapAll$RECORD_ID = NULL

gpraAdult3monthRedCapAll$REDCAP_SURVEY_IDENTIFIER
```
Grab the time stamp and part id and break out the time stamp
```{r}
gpraAdult3monthRedCapAll = data.frame(gpraAdult3monthRedCapAll$REDCAP_SURVEY_IDENTIFIER,gpraAdult3monthRedCapAll$NATIONAL_MINORITY_SAHIV_PREVENTION_INITIATIVE_ADUL_TIMESTAMP) 

colnames(gpraAdult3monthRedCapAll) = c("PARTID", "TimeStamp")
head(gpraAdult3monthRedCapAll)

# Ok need to separate by space first then get rid of actual time
library(dplyr)
library(reshape2)
test = gpraAdult3monthRedCapAll$TimeStamp

test = colsplit(test, " ", c("Date", "Time"))
test$Time = NULL
test =data.frame(test)
write.csv(test, "test.csv", row.names = FALSE)
test = read.csv("test.csv", header = TRUE) 
test = colsplit(test$Date, "/", c("MONTH", "DAY", "YEAR"))
test
test = as.Date(paste(test$YEAR, test$MONTH, test$DAY, sep = "/"))

```



