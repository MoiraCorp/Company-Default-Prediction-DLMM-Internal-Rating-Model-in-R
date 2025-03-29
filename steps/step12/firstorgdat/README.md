## First run LDA on original data

### Running LDA with “a priori” probabilities deduced from the size of the GOOD-BAD classes in the “observed” population

We use the cbind() and lda() functions from the MASS R package -> https://cran.r-project.org/web/packages/MASS/index.html

> library(MASS) <br>
> wcs2trainL <- cbind(wcs2train$BADGOOD, wcs2train.ratios) <br>
> names(wcs2trainL)[1] = "BADGOOD"

<em>NOTE</em>: We eliminate companies (idem, rows) with NA values.

By default, the “a priori” probalities are proportional to the number of GOOD and BAD in the input datatable.<br>
We select option: CV = TRUE in oredre to perform one-off classification on each of the companies after model determination

> w <- na.omit(wcs2trainL) <br>
> z <- lda(BADGOOD ~ ., data=w, CV = TRUE) <br>
> **Warning message:** <br>
> **In lda.default(x, grouping, ...) : variables are collinear** <br>
> tab <- table(w$BADGOOD, z$class) <br>
> tab <br>

##### <em>The printed output is:

|           | "Bad"    | "Good"       | 
| --------- | ------- | ------------ |
| "Bad"        |  2  | 49  |
| "Good"   | 4  | 1212   |

</em>
<em>NOTE</em>: The LDA signals that a certain number of variables are colinear

### Running LDA with equal “a priori” probabilities

The “a priori” probabilities are specified in the list: prior = c(1,1)/2

> w <- na.omit(wcs2trainL) <br>
> z <- lda(BADGOOD ~ ., data=w, prior = c(1,1)/2, CV = TRUE) <br>
> **Warning message:** <br>
> **In lda.default(x, grouping, ...) : variables are collinear** <br>
> tab <- table(w$BADGOOD, z$class) <br>
> tab <br>

##### <em>The printed output is:

|           | "Bad"    | "Good"       | 
| --------- | ------- | ------------ |
| "Bad"        |  7  | 44  |
| "Good"   | 146  | 1070   |

<em>NOTE</em>: One can witness **an IMPROVEMENT when using EQUAL “A PRIORI” PROBABILITIES**



