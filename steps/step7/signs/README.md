## Comparison between BADGOOD distribution and the sign of ROE numerator and denominator

In the W_CS_1_AnalysisSampleDataSet_2B.xls database: ROE-86 = NPROF-85 / EQUITY-29<br>


We are using the describe() function from the R psych package -> https://cran.r-project.org/web/packages/psych/index.html<br>
in order obtain descriptive statistics for each of the variables of the  wcs2train (Version 2B) table.<br>

> library(psych)<br>
> deswcs2train_2B <- describe(wcs2train)<br>
> write.csv(deswcs2train_2B, file = "C:/Projets_En_Cours/AI_MTPL/UCI_Internal_Ratings/R Notes/deswcs2train_2B.csv")<br>

The available statistics gerneratd by the describe function are:
 - vars: 	index of variable in table
 - n: 	number of valid members (except for NA)
 - mean: 	mean or average
 - sd: 	standard deviation
 - median: 	median
 - trimmed: trimmed mean (with trim defaulting to .1) ?
 - mad: 	median absolute deviation (from the median)
 - min: 	minimum value
 - max: 	maximum value
 - range: 	range length
 - skew: 	skew
 - kurtosis: kurtosis
 - se: 	r.m.s. error

 ##### <em>For  NPROF-85 and EQUITY-29 we get the following printed results:
	<em>var		min		max		range<br>
	NPROF-85	-5379		5327		10706<br>
	EQUITY-29	-3685		152567	156252<br></em>

> NPROFsign <- cut(wcs2train$NPROF, breaks=c(-Inf, -1, 0, Inf), labels=c("-", "0", "+"), include.lowest=FALSE)
> summary(NPROFsign)
##### <em>The printed output is:
   \-    0    \+<br>
 230   16 1025</em>

> EQUITYsign <- cut(wcs2train$EQUITY, breaks=c(-Inf, -1, 0, Inf), labels=c("-", "0", "+"), include.lowest=FALSE)
> summary(EQUITYsign)
##### <em>The printed output is:               	
   \-    0    \+<br>
 200    6 1065</em>

> STATUS <- wcs2train$BADGOOD
> ROEsign <- cbind(STATUS=levels(STATUS)[STATUS], NPROFsign=levels(NPROFsign)[NPROFsign], EQUITYsign=levels(EQUITYsign)[EQUITYsign])
> summary(ROEsign)
##### <em>The printed output is:
 STATUS     NPROFsign EQUITYsign<br>
 "Bad" :  51   \-: 230    \-: 200   
 "Good":1220   \+:1025    \+:1065   
               0:  16    0:   6</em>

> ROEsign <- cbind(STATUS=levels(STATUS)[STATUS], NPROFsign=levels(NPROFsign)[NPROFsign], EQUITYsign=levels(EQUITYsign)[EQUITYsign])
> summary(ROEsign)
##### <em>The printed output is:
 STATUS     NPROFsign EQUITYsign<br>
 "Bad" :  51   \-: 230    \-: 200    
 "Good":1220   +:1025    +:1065    
               0:  16    0:   6</em>
 #### Building a 3-way count table mimicking that of Table 4.18, page 159

> EQUNPRvSTATUS <- xtabs(~ EQUITYsign + NPROFsign + STATUS, ROEsign)<br>
> EQUNPRvSTATUS, , STATUS = "Bad"
##### <em>The printed output is:
NPROFsign<br>
EQUITYsign   \-   \+   0<br>
         \-   4   9   0<br>
         \+  14  24   0<br>
         0   0   0   0</em>

> EQUNPRvSTATUS <- xtabs(~ EQUITYsign + NPROFsign + STATUS, ROEsign)<br>
> EQUNPRvSTATUS, , STATUS = "Good"
##### <em>The printed output is:
NPROFsign<br>
EQUITYsign   \-   \+   0<br>
         \-  47 138   2<br>
         \+ 165 848  14<br>
         0   0   6   0
         
 



 
