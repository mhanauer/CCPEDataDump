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
gpraAdultAllUpload = gpraAdultAllUpload[1:882,] 

# Get INSTRMNT_LANG.x/y 1's 
gpraAdultAllUpload$INSTRMNT_LANG.x = rep(1, dim(gpraAdultAllUpload)[1])
gpraAdultAllUpload$INSTRMNT_LANG.y = rep(1, dim(gpraAdultAllUpload)[1])

# SP021203 for grant id
gpraAdultAllUpload$GRANT_ID.x = rep("SP021203", dim(gpraAdultAllUpload)[1])
gpraAdultAllUpload$GRANT_ID.y = rep("SP021203", dim(gpraAdultAllUpload)[1])

head(gpraAdultAllUpload)
```
Ok try to get a long format
```{r}
gpraAdultAllUploadTest = reshape(gpraAdultAllUpload, varying = list(c("INSTRMNT_LANG.x", "INSTRMNT_LANG.y"), c("LANG_OTHER.x", "LANG_OTHER.y"), c("GRANT_ID.x", "GRANT_ID.y"), c("DESIGNGRP.x", "DESIGNGRP.y"), c("MONTH.x", "MONTH.y"), c("DAY.x", "DAY.y"), c("YEAR.x", "YEAR.y"), c("INTTYPE.x", "INTTYPE.y"), c("INTERVENTION_A.x", "INTERVENTION_A.y"), c("INTERVENTION_B.x", "INTERVENTION_B.y"), c("INTERVENTION_C.x", "INTERVENTION_C.y"), c("GENDER.x", "GENDER.y"), c("YOB.x", "YOB.y"), c("E_NONHISPAN.x", "E_NONHISPAN.y"), c("E_MEXICAN.x", "E_MEXICAN.y"), c("E_PUERTRICAN.x", "E_PUERTRICAN.y"), c("E_CUBAN.x", "E_CUBAN.y"), c("E_OTHERHISPAN.x", "E_OTHERHISPAN.y"), c("R_WHITE_N.x", "R_WHITE_N.y"), c("R_BLACK_N.x", "R_BLACK_N.y"), c("R_AMERINALSK_N.x", "R_AMERINALSK_N.y"), c("R_ASIAIN_N.x", "R_ASIAIN_N.y"), c("R_CHINESE_N.x", "R_CHINESE_N.y"), c("R_FILIP_N.x", "R_FILIP_N.y"), c("R_JAPAN_N.x", "R_JAPAN_N.y"), c("R_KOR_N.x", "R_KOR_N.y"), c("R_VIETNAM_N.x", "R_VIETNAM_N.y"), c("R_OTHERASIA_N.x", "R_OTHERASIA_N.y"), c("R_HAW_N.x", "R_HAW_N.y"), c("R_GUAM_N.x", "R_GUAM_N.y"), c("R_SAMO_N.x", "R_SAMO_N.y"), c("R_OTHERPI_N.x"), c("SEX_PR.x", "SEX_PR.y"), c("SPEAK_ENG.x", "SPEAK_ENG.y"), c("LANG.x", "LANG.y"), c("EDLEVEL_N.x", "EDLEVEL_N.y"), c("COLLEGE.x", "COLLEGE.y"), c("EMPLOY_N.x", "EMPLOY_N.y"), c("PMECONDITION.x", "PMECONDITION.y"), c("JAILTIME_N.x", "JAILTIME_N.y"), c("MILSERVENO.x", "MILSERVENO.y"), c("MILSERVEARM.x", "MILSERVEARM.y"), c("MILSERVERES.x", "MILSERVERES.y"), c("MILSERVENG.x", "MILSERVENG.y"), c("ACTIVE.x", "ACTIVE.y"), c("DEPLOYEDNO.x", "DEPLOYEDNO.y"), c("DEPLOYEDIRAQ.x", "DEPLOYEDIRAQ.y"), c("DEPLOYEDPERS.x", "DEPLOYEDPERS.y"), c("DEPLOYEDASIA.x", "DEPLOYEDASIA.y"), c("DEPLOYEDKOR.x", "DEPLOYEDKOR.y"), c("DEPLOYEDWWII.x", "DEPLOYEDWWII.y"), c("DEPLOYEDOTH.x", "DEPLOYEDOTH.y"), c("OTHACTIVE.x", "OTHACTIVE.y"), c("SERVREL1.x","SERVREL1.y"), c("SERVREL1_OTHER.x", "SERVREL1_OTHER.y"), c("SERVREL2.x", "SERVREL2.y"), c("SERVREL2_OTHER.x", "SERVREL2_OTHER.y"), c("SERVREL3.x", "SERVREL3.y"), c("SERVREL3_OTHER.x", "SERVREL3_OTHER.y"), c("SERVREL4.x", "SERVREL4.y"), c("SERVREL4_OTHER.x", "SERVREL4_OTHER.y"), c("SERVREL5.x", "SERVREL5.y"), c("SERVREL5_OTHER.x", "SERVREL5_OTHER.y"), c("SERVREL6.x", "SERVREL6.y"), c("SERVREL6_OTHER.x", "SERVREL6_OTHER.y"), c("RSKCIG.x", "RSKCIG.y"), c("RSKMJ.x", "RSKMJ.y"), c("RSKALC.x", "RSKALC.y"), c("PEERBINGE_A.x", "PEERBINGE_A.y"), c("WRGBINGE_A.x", "WRGBINGE_A.y")))
```



 
