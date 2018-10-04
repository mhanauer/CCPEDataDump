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
gpraAdultAllUploadTest = reshape(gpraAdultAllUpload, varying = list(c("INSTRMNT_LANG.x", "INSTRMNT_LANG.y"), c("LANG_OTHER.x", "LANG_OTHER.y"), c("GRANT_ID.x", "GRANT_ID.y"), c("DESIGNGRP.x", "DESIGNGRP.y"), c("MONTH.x", "MONTH.y"), c("DAY.x", "DAY.y"), c("YEAR.x", "YEAR.y"), c("INTTYPE.x", "INTTYPE.y"), c("INTERVENTION_A.x", "INTERVENTION_A.y"), c("INTERVENTION_B.x", "INTERVENTION_B.y"), c("INTERVENTION_C.x", "INTERVENTION_C.y"), c("GENDER.x", "GENDER.y"), c("YOB.x", "YOB.y"), c("E_NONHISPAN.x", "E_NONHISPAN.y"), c("E_MEXICAN.x", "E_MEXICAN.y"), c("E_PUERTRICAN.x", "E_PUERTRICAN.y"), c("E_CUBAN.x", "E_CUBAN.y"), c("E_OTHERHISPAN.x", "E_OTHERHISPAN.y"), c("R_WHITE_N.x", "R_WHITE_N.y"), c("R_BLACK_N.x", "R_BLACK_N.y"), c("R_AMERINALSK_N.x", "R_AMERINALSK_N.y"), c("R_ASIAIN_N.x", "R_ASIAIN_N.y"), c("R_CHINESE_N.x", "R_CHINESE_N.y"), c("R_FILIP_N.x", "R_FILIP_N.y"), c("R_JAPAN_N.x", "R_JAPAN_N.y"), c("R_KOR_N.x", "R_KOR_N.y"), c("R_VIETNAM_N.x", "R_VIETNAM_N.y"), c("R_OTHERASIA_N.x", "R_OTHERASIA_N.y"), c("R_HAW_N.x", "R_HAW_N.y"), c("R_GUAM_N.x", "R_GUAM_N.y"), c("R_SAMO_N.x", "R_SAMO_N.y"), c("R_OTHERPI_N.x"), c("SEX_PR.x", "SEX_PR.y"), c("SPEAK_ENG.x", "SPEAK_ENG.y"), c("LANG.x", "LANG.y"), c("EDLEVEL_N.x", "EDLEVEL_N.y"), c("COLLEGE.x", "COLLEGE.y"), c("EMPLOY_N.x", "EMPLOY_N.y"), c("PMECONDITION.x", "PMECONDITION.y"), c("JAILTIME_N.x", "JAILTIME_N.y"), c("MILSERVENO.x", "MILSERVENO.y"), c("MILSERVEARM.x", "MILSERVEARM.y"), c("MILSERVERES.x", "MILSERVERES.y"), c("MILSERVENG.x", "MILSERVENG.y"), c("ACTIVE.x", "ACTIVE.y"), c("DEPLOYEDNO.x", "DEPLOYEDNO.y"), c("DEPLOYEDIRAQ.x", "DEPLOYEDIRAQ.y"), c("DEPLOYEDPERS.x", "DEPLOYEDPERS.y"), c("DEPLOYEDASIA.x", "DEPLOYEDASIA.y"), c("DEPLOYEDKOR.x", "DEPLOYEDKOR.y"), c("DEPLOYEDWWII.x", "DEPLOYEDWWII.y"), c("DEPLOYEDOTH.x", "DEPLOYEDOTH.y"), c("OTHACTIVE.x", "OTHACTIVE.y"), c("SERVREL1.x","SERVREL1.y"), c("SERVREL1_OTHER.x", "SERVREL1_OTHER.y"), c("SERVREL2.x", "SERVREL2.y"), c("SERVREL2_OTHER.x", "SERVREL2_OTHER.y"), c("SERVREL3.x", "SERVREL3.y"), c("SERVREL3_OTHER.x", "SERVREL3_OTHER.y"), c("SERVREL4.x", "SERVREL4.y"), c("SERVREL4_OTHER.x", "SERVREL4_OTHER.y"), c("SERVREL5.x", "SERVREL5.y"), c("SERVREL5_OTHER.x", "SERVREL5_OTHER.y"), c("SERVREL6.x", "SERVREL6.y"), c("SERVREL6_OTHER.x", "SERVREL6_OTHER.y"), c("RSKCIG.x", "RSKCIG.y"), c("RSKMJ.x", "RSKMJ.y"), c("RSKALC.x", "RSKALC.y"), c("PEERBINGE_A.x", "PEERBINGE_A.y"), c("WRGBINGE_A.x", "WRGBINGE_A.y"), c("WRGSEX_UNP_A.x", "WRGSEX_UNP_A.y"), c("RSKANYSEX_UNP.x", "RSKANYSEX_UNP.y"), c("RSKSEX_ALCDRG.x", "RSKSEX_ALCDRG.y"), c("RSKNDL_SHR.x", "RSKNDL_SHR.y"), c("CNTRL_REFUSEMOOD.x", "CNTRL_REFUSEMOOD.y"), c("CNTRL_WAITCNDM.x", "CNTRL_WAITCNDM.x"), c("CNTRL_TREAT.x", "CNTRL_TREAT.y"), c("CNTRL_SEXPRAC.x", "CNTRL_SEXPRAC.y"), c("CNTRL_ASKCNDM.x", "CNTRL_ASKCNDM.y"), c("CNTRL_REFUSECNDM.x", "CNTRL_REFUSECNDM.y"), c("HIV_SICK_N.x", "HIV_SICK_N.y"), c("HIV_GAYSEX_N.x", "HIV_GAYSEX_N.y"), c("HIV_BCPILL_N.x", "HIV_BCPILL_N.y"), c("HIV_DRGS_N.x", "HIV_DRGS_N.y"), c("HIV_CURE_N.x", "HIV_CURE_N.y"), c("KNOW_HIV.x", "KNOW_HIV.y"), c("KNOW_SA.x", "KNOW_SA.y"), c("GET_MEDHLP.x", "GET_MEDHLP.y"), c("LIFE_RESP_SERV.x", "LIFE_RESP_SERV.y"), c("RESPECT_RACE.x", "RESPECT_RACE.y"), c("RESPECT_REL.x", "RESPECT_REL.y"), c("RESPECT_GENDER.x", "RESPECT_GENDER.y"), c("RESPECT_AGE.x", "RESPECT_AGE.y"), c("RESPECT_SEXPR.x", "RESPECT_SEXPR.y"), c("RESPECT_DISABLE.x", "RESPECT_DISABLE.y"), c("RESPECT_MH.x", "RESPECT_MH.y"), c("RESPECT_HIV.x", "RESPECT_HIV.y"), c("RESPECT_NONE.x", "RESPECT_NONE.y"), c("HIV_RESULTS_N.x", "HIV_RESULTS_N.y"), c("TALK_ALLPERS_N.x", "TALK_ALLPERS_N.y"), c("REL_IMP.x", "REL_IMP.y"), c("CIG30D.x", "CIG30D.y"), c("TOB30D.x", "TOB30D.y"), c("VAP30D.x", "VAP30D.y"), c("ALC30D.x", "ALC30D.x"), c("BINGE530D.x", "BINGE530D.y"), c("MJ30D.x", "MJ30D.y"), c("ILL30D.x", "ILL30D.y"), c("RX30D.x", "RX30D.y"), c("SPICE30D.x", "SPICE30D.y"), c("INJECT30D.x", "INJECT30D.y"), c("CUT_ALC.x", "CUT_ALC.y"), c("ANNOY_ALC.x", "ANNOY_ALC.y"), c("GUILT_ALC.x", "GUILT_ALC.y"), c("MORN_ALC.x", "MORN_ALC.y"), c("EMO_AFT.x", "EMO_AFT.y"), c("MENTLH30D.x", "MENTLH30D.y"), c("SEX_HAD.x", "SEX_HAD.y"), c("SEX_ANY30D.x", "SEX_ANY30D.y"), c("LASTSEX_UNP.x", "LASTSEX_UNP.y"), c("SEX_MALEEVER.x", "SEX_MALEEVER.y"), c("SEX_FEMALEEVER.x"), c("SEX_FEMALEEVER.y"), c("SEX_MNY_3MOS.x", "SEX_MNY_3MOS.y"), c("WHENSEX4STFF_UNP.x", "WHENSEX4STFF_UNP.y"), c("WHENSEXHIVSTD_UNP.x", "WHENSEXHIVSTD_UNP.y"), c("WHENSEXDRUG_UNP.x", "WHENSEXDRUG_UNP.y"), c("WHENSEXALCDRG.x", "WHENSEXALCDRG.y"), c("ANYABUSE_3M.x", "ANYABUSE_3M.y"), c("SEXUNWANT_12M.x", "SEXUNWANT_12M.y"), c("MSTATUS_N.x", "MSTATUS_N.y"), c("LIVE_N.x", "LIVE_N.y"), c("HOMETYPE_N.x", "HOMETYPE_N.x"), c("PARSUPB.x", "PARSUPB.y"), c("HINCOMEO_N.x", "HINCOMEO_N.y"), c("HC_HAVE_N.x", "HC_HAVE_N.y"), c("DRGTST.x", "DRGTST.y"), c("SVY_TRUTH.x", "SVY_TRUTH.y")), direction = "long", times =c(1,3))



```




