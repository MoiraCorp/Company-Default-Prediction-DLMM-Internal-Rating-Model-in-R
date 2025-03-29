## LDA on full author’s datatable

The table wcs8train.vars contains the complete data set over all the ratios
	
<em>NOTE : </em> **IMPORTANT: The variable TAXESONG3A IS CONSTANT = 0** thus it must be removed before performing the LDA. This variable is situated at index = 55 

> library(MASS) <br>
> w <- na.omit(wcs8train.vars[c(1:54,56:74)]) <br>
> z <- lda(BADGOOD ~ ., data=w, prior = c(1,1)/2, CV = TRUE) <br>
> **Warning message:** <br>
> **In lda.default(x, grouping, ...) : variables are collinear** <br>
> table(w$BADGOOD, z$class)

 ##### <em>The printed output is:

|           | "Bad"    | "Good"       | 
| --------- | ------- | ------------ |
| "Bad"        |  19  | 32  |
| "Good"   | 162  | 1054   |

em>NOTE : </em> This result is **SIMILAR to the one obtained by the author using Stepwise LDA determined formula**
