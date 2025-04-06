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

#### Proceeding with the Gauss Copula encoding <br>
> \# Loading the Gauss Copula encoding table <br>
> tgauss <- c(  0, 14, 24, 31, 36, 40, 43, 46, 48, 50, 52, 54, 56, 58, 59, 61, <br>
        62, 63, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, <br>
        79, 79, 80, 81, 82, 82, 83, 84, 85, 85, 86, 87, 87, 88, 89, 89, <br>
        90, 90, 91, 92, 92, 93, 93, 94, 95, 95, 96, 96, 97, 97, 98, 98, <br>
        99, 99,100,100,101,101,102,102,103,103,104,104,105,105,106,106, <br>
       107,107,108,108,109,109,110,110,111,111,111,112,112,113,113,114, <br>
       114,115,115,115,116,116,117,117,118,118,118,119,119,120,120,121, <br>
       121,121,122,122,123,123,124,124,124,125,125,126,126,126,127,127, <br>
       128,128,129,129,129,130,130,131,131,131,132,132,133,133,134,134, <br>
       134,135,135,136,136,137,137,137,138,138,139,139,140,140,140,141, <br>
       141,142,142,143,143,144,144,144,145,145,146,146,147,147,148,148, <br>
       149,149,150,150,151,151,152,152,153,153,154,154,155,155,156,156, <br>
       157,157,158,158,159,159,160,160,161,162,162,163,163,164,165,165, <br>
       166,166,167,168,168,169,170,170,171,172,173,173,174,175,176,176, <br>
       177,178,179,180,181,182,183,184,185,186,187,188,189,190,192,193, <br>
       194,196,197,199,201,203,205,207,209,212,215,219,224,231,241,255) <br>
> bins_cut = 255 <br>
> \# Encoding all ratios using a Gaussian anamorphosis <br>
> wcs9train.ratiosG <- wcs9train.ratios <br>
> for(i in 1:34){ <br>
	\# Calling .bincode() with quantile(na.rm = TRUE) remove NA and right = TRUE, include.lowest = TRUE, thus generating 256 entries (0 to 255) <br>
	rm(QUANT256) <br>
	QUANT256 <- .bincode(wcs9train.ratios[,i], quantile(wcs9train.ratios[,i], probs = seq(0, 1, 1/bins_cut), na.rm = TRUE), right = TRUE, include.lowest = TRUE) <br>
	for(j in 1:length(QUANT256)){ <br>
		wcs9train.ratiosG[j,i] <- tgauss[QUANT256[j]] <br>
	} <br>
} <br>
