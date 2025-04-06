## Using Gaussian Copula encoding for LDA

> \# Data preparation <br>
> \# The names of variables have been simplified according to W_CS_1_Schema.xls (Done using OpenOffice) <br>
> \# BADGOOD variable values have been transformed : 0 -> "Good" and 1 -> "Bad" (Done using OpenOffice) <br>
> wcs9train <- read.csv("C:/Projets_En_Cours/AI_MTPL/UCI_MTPL_Internal_Ratings/SPSS-PASW/W_CS_1_AnalysisSampleDataSet_9MDAbin.csv", header=TRUE, sep=",") <br>
> summary(wcs9train$BADGOOD)

##### <em>The printed output is: <br>
| Group code | "Bad" | "Good" |
| ---------- | ----- | ------ |
|  | 51 | 1221 |
</em>
