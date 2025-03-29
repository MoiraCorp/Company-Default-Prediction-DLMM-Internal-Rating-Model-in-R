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

Values calculated in each step of the selection procedure: 


