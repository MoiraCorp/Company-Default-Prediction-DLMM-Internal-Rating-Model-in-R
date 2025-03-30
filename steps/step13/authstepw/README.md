## Applying authors recommended stepwise LDA performed on datatable wcs8train

For this purpose, we are using the klaR R package, the function greedy.wilks performs Stepwise LDA using the Wilk's Lambda criterion, method used by the authors (page 190)
The kLAR package is downloaded from: https://cran.r-project.org/web/packages/klaR/index.html and locally installed.

> library(klaR) <br>
> w <- na.omit(wcs8train.vars[c(1:54,56:74)]) <br>
> gw_obj <- greedy.wilks(BADGOOD ~ ., data =w, niveau = 0.1) <br>

Crashed on: **Error in summary.manova(e2, test = "Wilks") : residuals have rank 7 < 8**<br>
<em>NOTE : </em> If we **DO NOT SPECIFY, “a priori” probabilities, the lda function displays the coefficients of the regression formula**

> w <- na.omit(wcs8train.vars[c(1:54,56:74)]) <br>
> z <- lda(BADGOOD ~ ROETR + IEONLIAB + V95A3A + EQUITYON + EQUITYON3A + 
    SALESBin2cl1 + ROAMINUS, data = wcs8train.vars, na.action = "na.omit") <br>
> **Warning message:** <br>
> **In lda.default(x, grouping, ...) : variables are collinear** <br>
> table(w$BADGOOD, z$class)

 ##### <em>The printed output is:</em>

Prior probabilities of groups:

|           | "Bad"    | "Good"       | 
| --------- | ------- | ------------ |
|         |  0.04009434  | 0.95990566  |

Coefficients of linear discriminants:

|           | LD1    |
| --------- | ------- |
| ROETR        |   9.964643e-05  |
| IEONLIAB     |  -7.999371e-02  |
| V95A3A       |  -3.570714e-03  |
| EQUITYON     |  -2.099401e-03  |
| EQUITYON3A   |   8.076022e-03  |
| SALESBin2cl1 |   5.146604e-01  |
| ROAMINUS     |  -1.457695e-03  |

Comparative results on regression coefficients presented by author on page 194 as “Canonical discriminant function coefficients:

|   Ratio        | Our results    | Authors' results       | 
| --------- | ------- | ------------ |		
|  ROOETR	 |  0	 |  0  |
|  IEONLIAB	 |  -0.08	 |  0.08  |
|  V95A3A	 |  -0.0036	 |  0.004  |
|  EQUITYON	 |  -0.0021	 |  0.002  |
|  EQUITYON3A	 |  0.0008	 |  -0.008  |
|  SALESBin2cll	 |  0.514	 |  -0.512  |
|  ROAMINUS	 |  -0.0014	 |  0.001  |

<em>NOTE : </em> **The RESULTS ARE IDENTICAL**

We compute the final comparative cross-classification table

> z <- lda(BADGOOD ~ ROETR + IEONLIAB + V95A3A + EQUITYON + EQUITYON3A + SALESBin2cl1 + ROAMINUS, data= wcs8train.vars, na.action="na.omit", prior = c(1,1)/2, CV = TRUE) <br>
> tab <- table(wcs8train.vars$BADGOOD, z$class) <br>
> tab

 ##### <em>The printed output is:

|           | "Bad"    | "Good"       | 
| --------- | ------- | ------------ |
| "Bad"        |  14  | 37  |
| "Good"   | 142  | 1079   |

<em>NOTE : </em> **VERY SIMILAR to the one obtained by the authors (page 201)**







