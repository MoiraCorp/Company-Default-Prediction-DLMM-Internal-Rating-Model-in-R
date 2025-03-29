## Stepwise LDA on original data

In klaR R package, the function greedy.wilks performs Stepwise LDA using the Wilk's Lambda criterion, method used by the authors (page 190)

The kLAR package is downloaded from: https://cran.r-project.org/web/packages/klaR/index.html
and locally installed.<br>
It also needs as dependencies the following other packages: Also needs as dependency: MASS, combinat, questionr and MiniUI<br>

We use the cbind() and lda() functions from the MASS R package -> https://cran.r-project.org/web/packages/MASS/index.html<br>
The combinat package is downloaded from: -> https://cran.r-project.org/web/packages/combinat/index.html<br>
The questionr package is downloaded from: -> https://cran.r-project.org/web/packages/questionr/index.html<br>
The MiniUI package is downloaded from: -> https://pbil.univ-lyon1.fr/CRAN/bin/windows/contrib/3.4/miniUI_0.1.1.1.zip<br>

> library(klaR) <br>
> wcs2trainL <- cbind(wcs2train$BADGOOD, wcs2train.ratios) <br>
> names(wcs2trainL)[1] = "BADGOOD" <br>
> w <- na.omit(wcs2trainL) <br>
> gw_obj <- greedy.wilks(BADGOOD ~ ., data = w, niveau = 0.1) <br>
> gw_obj <br>

> Formula containing included variables:  <br>
> BADGOOD ~ ROETR + IEONLIAB + EQUITYON + V110A + TRADEPA. + ASSETSTU <br>
> <environment: 0x0000000004640b30> <br>

Values calculated in each step of the selection procedure: <em>

| Ratios    | Wilks.lambda    | F.statistics.overall    | p.value.overall    | F.statistics.diff    | p.value.diff    |
| ------------ | ------------ | ------------ | ------------- | ------------ | ------------ |
|    ROETR      |    0.9813240    | 24.07480     | 1.047297e-06    | 24.074799    | 1.047297e-06    |
|  IEONLIAB     |    0.9628733    | 24.36883     | 4.127506e-11    | 24.220942    | 9.721454e-07    |
|  EQUITYON     |    0.9554423    | 19.63360     | 1.921645e-12    |  9.822947    | 1.763140e-03    |
|     V110A     |    0.9521049    | 15.87107     | 1.108036e-12    |  4.423778    | 3.563887e-02    |
|  TRADEPA.     |    0.9489687    | 13.56220     | 6.535577e-13    |  4.167383    | 4.141703e-02    |
|  ASSETSTU     |    0.9453482    | 12.14038     | 2.639645e-13    |  4.825591    | 2.822170e-02    |
</em>

We follow by using the “suite” of Ratio Variables determined by stepwise LDA

> z <- lda(BADGOOD ~ ROETR + IEONLIAB + EQUITYON + V110A + TRADEPA. + ASSETSTU, data=w, prior = c(1,1)/2, CV = TRUE) <br>
> tab <- table(w$BADGOOD, z$class) <br>
> tab

##### <em>The printed output is:

|           | "Bad"    | "Good"       | 
| --------- | ------- | ------------ |
| "Bad"        |  6  | 45  |
| "Good"   | 118  | 1098   |

<em>NOTE : </em> The result **somewhat identical to that of the first run of full LDA on original data** with a slight improvement on the GOOD class

</em>Although the list of variables by declining Wilks.lambda looks similar to that of the author in
Table 4.28 Stepwise statistics (page 190) it is not fully identical. <br>
That of the author is:



