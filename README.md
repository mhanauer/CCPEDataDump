---
title: "CCPEDatUpload"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Data upload
```{r}
setwd("S:/Indiana Research & Evaluation/CCPE/DataUploadDosage")
REDCap_Data_CCPE_Upload_5_220 = read.csv("REDCap_Data_CCPE_Upload_5_20.csv", header = TRUE)
base_date =  str_split_fixed(REDCap_Data_CCPE_Upload_5_220$baseline_completion_date, "/",n = 3)
base_date = data.frame(base_date)
names(base_date) = c("MONTH", "DAY", "YEAR")
write.csv(base_date, "base_date.csv", row.names = FALSE)
bday =  mdy(REDCap_Data_CCPE_Upload_5_220$BirthDateMonthYear)
bday = floor_date(bday, unit = "month")
bday =  str_split_fixed(bday, "-",n = 3)
bday = data.frame(bday)
colnames(bday) = c("YEAR", "MONTH", "DAY")  
bday = paste0(bday$MONTH, bday$YEAR)
write.csv(bday, "bday.csv", row.names = FALSE)
```

