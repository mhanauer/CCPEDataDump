---
title: "CCPEDDataDump"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

Figure out what aspects you are missing
You need to get rid of na's for grant ID
Get rid of 1750 person
1924 onward you need numbers for these INSTRMNT_LANG.x	LANG_OTHER.x
You need long form 
Change names (get rid of x)

Use gpraAdultAll
First getting rid of one NA all value
```{r}
gpraAdultAllUpload =  gpraAdultAll[-c(641,1),]


# Next there are bunch of NA's need to get rid of them
# Data beyond this is point is NA 
dim(gpraAdultAllUpload)
gpraAdultAllUpload = gpraAdultAllUpload[1:990,] 

# Get INSTRMNT_LANG.x/y 1's 
gpraAdultAllUpload$INSTRMNT_LANG.x = rep(1, dim(gpraAdultAllUpload)[1])
gpraAdultAllUpload$INSTRMNT_LANG.y = rep(1, dim(gpraAdultAllUpload)[1])

# SP021203 for grant id
gpraAdultAllUpload$GRANT_ID.x = rep("SP021203", dim(gpraAdultAllUpload)[1])
gpraAdultAllUpload$GRANT_ID.y = rep("SP021203", dim(gpraAdultAllUpload)[1])

gpraAdultAllUploadPre = gpraAdultAllUpload[c(1:139)]

head(gpraAdultAllUploadPre)


gpraAdultAllUploadPost = gpraAdultAllUpload[c(1, 140:277)]

head(gpraAdultAllUploadPost)

# Ok so split apart the data with just the dates or one date if there is an NA na.omit the data then merge back with ids so need ids for both
gpraAdultAllUploadPostDate = data.frame(PARTID = gpraAdultAllUploadPost$PARTID, MONTH =  gpraAdultAllUploadPost$MONTH.y, DAY  = gpraAdultAllUploadPost$DAY.y, YEAR = gpraAdultAllUploadPost$YEAR.y) 

gpraAdultAllUploadPostDate = na.omit(gpraAdultAllUploadPostDate)

gpraAdultAllUploadPost = merge(gpraAdultAllUploadPostDate, gpraAdultAllUploadPost, all.x = TRUE, by = "PARTID")

names(gpraAdultAllUploadPre) = gsub(".x", "", names(gpraAdultAllUploadPre))

names(gpraAdultAllUploadPost) = gsub(".y", "", names(gpraAdultAllUploadPost))

head(gpraAdultAllUploadPost)
gpraAdultAllUploadPost = gpraAdultAllUploadPost[,-c(2:4)]



write.csv(gpraAdultAllUploadPre, "gpraAdultAllUploadPre.csv", row.names = FALSE)
write.csv(gpraAdultAllUploadPost, "gpraAdultAllUploadPost.csv", row.names = FALSE)

gpraAdultAllUpload = rbind(gpraAdultAllUploadPre, gpraAdultAllUploadPost)
dim(gpraAdultAllUploadPre)
dim(gpraAdultAllUploadPost)

write.csv(gpraAdultAllUpload, "gpraAdultAllUpload.csv", row.names = FALSE)

```
