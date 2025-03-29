## First run LDA on original data

### Running LDA with “a priori” probabilities deduced from the size of the GOOD-BAD classes in the “observed” population

> library(MASS) <br>
> wcs2trainL <- cbind(wcs2train$BADGOOD, wcs2train.ratios) <br>
> names(wcs2trainL)[1] = "BADGOOD"

<em>NOTE</em>: We eliminate companies (idem, rows) with NA values.

By default, the “a priori” probalities are proportional to the number of GOOD and BAD in the input datatable.<br>
We select option: CV = TRUE in oredre to perform one-off classification on each of the companies after model determination

> w <- na.omit(wcs2trainL) <br>
> z <- lda(BADGOOD ~ ., data=w, CV = TRUE) <br>
> Warning message: <br>
> In lda.default(x, grouping, ...) : variables are collinear <br>
> tab <- table(w$BADGOOD, z$class) <br>
> tab <br>

##### <em>The printed output is:

|           | "Bad"    | "Good"       | 
| --------- | ------- | ------------ |
| "Bad"        |  2  | 49  |
| "Good"   | 4  | 1212   |

</em>


### Running LDA with equal “a priori” probabilities

