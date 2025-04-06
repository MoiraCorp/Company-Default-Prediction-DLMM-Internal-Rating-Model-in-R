## Using Gaussian Copula encoding for LDA

#### Data preparation <br>
> \# The names of variables have been simplified according to W_CS_1_Schema.xls (Done using OpenOffice) <br>
> \# BADGOOD variable values have been transformed : 0 -> "Good" and 1 -> "Bad" (Done using OpenOffice) <br>
> wcs9train <- read.csv("C:/Projets_En_Cours/AI_MTPL/UCI_MTPL_Internal_Ratings/SPSS-PASW/W_CS_1_AnalysisSampleDataSet_9MDAbin.csv", header=TRUE, sep=",") <br>
> summary(wcs9train$BADGOOD)

##### <em>The printed output is: <br>
| Group code | "Bad" | "Good" |
| ---------- | ----- | ------ |
|  | 51 | 1221 |
</em>

#### Selecting DL Ratios used for model determination from ROE to ROETR <br>
> ratiovars <- c(86:119) <br>
> wcs9train.ratios <- wcs9train[ratiovars] <br>
> sapply(wcs9train.ratios, class) <br>
>       ROE  EBITDAON       ROI       ROA      V89A       ROS  ASSETSTU  INVENTOR  RECEIVAB      V94A      V95A  PAYABLES  COMMERCI  IEONEBIT  NIEONEBI  IEONLIAB IEONFINA.    EXTRIC  <br>
> "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric"  <br>
>  TAXESONG  INTANGIB  TRADERE.     V110A  EQUITYON  TRADEPA.   DEBTEQU   CURRENT   QUICKRA  SALESONV  SALESMIN  ROAMINUS  EBITDAIE EQUILIABL DEBTEQUTR     ROETR  <br>
> "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "integer" <br>

> names(wcs9train.ratios) <br>
>  [1] "ROE"       "EBITDAON"  "ROI"       "ROA"       "V89A"      "ROS"       "ASSETSTU"  "INVENTOR"  "RECEIVAB"  "V94A"      "V95A"      "PAYABLES"  "COMMERCI"  "IEONEBIT"  "NIEONEBI"  <br>
> [16] "IEONLIAB"  "IEONFINA." "EXTRIC"    "TAXESONG"  "INTANGIB"  "TRADERE."  "V110A"     "EQUITYON"  "TRADEPA."  "DEBTEQU"   "CURRENT"   "QUICKRA"   "SALESONV"  "SALESMIN"  "ROAMINUS"  <br>
> [31] "EBITDAIE"  "EQUILIABL" "DEBTEQUTR" "ROETR" <br>

#### There are 34 columns <br>
> length(wcs9train.ratios) <br>
> [1] 34 <br>
