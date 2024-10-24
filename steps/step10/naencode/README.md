## Replacement of NA encoded outliers by multidimensional interpolation

In the previous section (step9), we have detected “extreme outliers” and encoded them as NA (not Available)<br>
However, most AI methods require the processing FULL datatables.<br>

In sction 4.5.9.1 Treatment of outliers and shapes of distributions (pp 164-165), the authors propose to “fill in” the masqued outliers with either the mean or the median of each of the Ratio Variable statistical distribution.<br>
Although it is common practice, <em>this method is based on a very thin probability theory argument</em>.<br><br>

The present dataset being essentially “multidimensional” it is better justified to proceed with the replacement of the NA values on the basis of the multidimensional relations existing between the Ratio Variables rather than processing them individually. In our case, all variables being numerical (see list below), we will apply Principal Componant Analysis (PCA) and follow by an "interpolation" of the missong valeus based on the PCA factor space vectors. This is performed using the missMDA R package (-> https://cran.r-project.org/web/packages/missMDA/index.html) following a PCA detremined using the FactoMineR R package (-> https://cran.r-project.org/web/packages/FactoMineR/index.html)

> \# Checking on variables type in the datatable<br>
> sapply(wcs2train.ratios.NA, class)<br>

##### <em>The printed output is:
&nbsp;      ROE  EBITDAON       ROI       ROA      V89A       ROS  ASSETSTU  INVENTOR  RECEIVAB      V94A      V95A  PAYABLES  COMMERCI  IEONEBIT  NIEONEBI  IEONLIAB IEONFINA.    EXTRIC  TAXESONG  INTANGIB  TRADERE.     V110A  EQUITYON TRADEPA.   DEBTEQU   CURRENT   QUICKRA  SALESONV  SALESMIN  ROAMINUS  EBITDAIE EQUILIABL DEBTEQUTR     ROET<br> 
&nbsp;      "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "integer"<br></em>

> \# Loading the necessary processing libraries<br>
> library(FactoMineR)<br>
> library(missMDA)<br>
> \# Estimate the number of PCA components necessary for a correct interpolation of NAs<br>
> ncomp <- estim_ncpPCA(wcs2train.ratios.NA)<br>
> \# Perform multidimensional interpolation of NA values using the MissMDA method<br>
> res.imp <- imputePCA(wcs2train.ratios.NA, ncp = ncomp$ncp)<br>
> \# Extract the NA completed rows<br>
> wcs2train.ratios.CT <- res.imp$completeObs[1:nrow(wcs2train.ratios.NA),]<br>

### Comparison of Ratio Variables range and statistics before and after “outliers” processing

We compare the Ratio Variables range and statistics between the corrected datatable wcs2train.ratios.CT and the uncorrected “original” datatable wcs2train.ratios using the built in summry() function from the standard R package.

> summary(wcs2train.ratios.CT)
> summary(wcs2train.ratios)

<em>NOTE: </em> We are not presenting here the printed ouputs of these two functions as they are being too bulky<br><br>
From these outputs it is esasy to see that the mean and median of each variable are comparable befaore and after processing but that the Min. and Max; “extreme” values have been somewhat “reined in” by the NA values replacement to the exception of vriaables such as V110A for which no outliers were detected (see previous section)

### Study of Ratio Variables correlation properties after “outliers” processing

<strong>A first approach is to graphically evaluate the multi-dimensional variable correlation chart</strong> produced by the chart.Correlation() function belonging to the erformanceAnalytics  R package (-> https://cran.r-project.org/web/packages/PerformanceAnalytics/index.html)

> library("PerformanceAnalytics")<br>
> chart.Correlation(wcs2train.ratios.CT, histogram=TRUE, pch=19)<br>

Illustrated in: Outlier-Treatment_Page165_AllvariableswithCT_CoorDiag.pdf
<img src="./assets/Outlier-Treatment_Page165_AllvariableswithCT_CoorDiag.JPG" alt="drawing" width="100%"/>

<em>NOTE :</em> In this chart, the cloud points of Corrected data are strikingly similar to those presented in the datatable with outliers masked as NAs (-> https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step9/naoutlr)

<strong>A second approach is to compare the pair-wise correlation coefficients between variables </strong> as it has been proposed in Step 8 (-> https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step8/allvar).<br> This process enables to determine potential groups of similar behaved variables. It is done using the corrplot R package (-> https://cran.r-project.org/web/packages/corrplot/vignettes/corrplot-intro.html) uagmented by the corr.pvalue() function (see -> https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step8/selectvar)

> cor.pvalue <- function(mat, ...) {<br> 
    mat <- as.matrix(mat)<br>
    n <- ncol(mat)<br>
    p.mat<- matrix(NA, n, n)<br>
    diag(p.mat) <- 0<br>
    for (i in 1:(n - 1)) {<br>
        for (j in (i + 1):n) {<br>
            tmp <- cor.test(mat[, i], mat[, j], ...)<br>
            p.mat[i, j] <- p.mat[j, i] <- tmp$p.value<br>
        }<br>
    }<br>
  colnames(p.mat) <- rownames(p.mat) <- colnames(mat)<br>
  p.mat
}<br>

> install.packages("corrplot")<br>
> library(corrplot)<br>
> corrprs	<- cor(wcs2train.ratios.CT, use="pairwise", method="pearson")<br>
> p.mat <- cor.pvalue(wcs2train.ratios.CT)<br>
> col <- colorRampPalette(c("#BB4444", "#fcc3b8", "#FFFFFF", "#add2f7", "#4fc69d"))<br>
> corrplot(corrprs, method="color", col=col(200), <br> 
         type="upper",<br> 
         addCoef.col = "black", \# Add coefficient of correlation<br>
         addCoefasPercent = TRUE,<br>
         tl.col="black", tl.srt=45, \# Text label color and rotation<br>
         \# Combine with significance
         p.mat = p.mat, sig.level = 0.01, insig = "blank",<br>
         \# hide correlation coefficient on the principal diagonal<br>
         diag=FALSE<br>
         )<br>
The graphics representation of the Pearson correlation between all the Corrected Ratio Variables is presented in: Outlier-Treatment_Page 165_Ratios_Correlation.pdf
<img src="./assets/Outlier-Treatment_Page 165_Ratios_Correlation.JPG" alt="drawing" width="60%"/>

<em>NOTE :</em> It is allmost identical to the correlation diagram established betwwen all Na masqued Ratio Variables (-> https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step8/allvar)<br>
This is conservation of corralation properties is inherent to the MissMCA interpolation method. This type of conservation is NOT guaranteed when using traditional mean-mode interpolation techniques.<bR>

<strong>A third approach for discovering potential groups of corralated variables is to use PCA.</strong> In the present study, the use of Principal Componant Analysis (PCA) is validated by the fact that all variables are numerical. For PCA we are gain using the FactoMineR R package ( -> https://cran.r-project.org/web/packages/FactoMineR/index.html) along with the factoextra R package ( -> https://cran.r-project.org/web/packages/factoextra/readme/README.html) for producing the factor plane displays<br>

        







