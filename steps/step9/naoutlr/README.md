## Masking outlier's values using the NA R notation

It is common practice to “mask out” outlier values for each of the Ratio variables in order to manipulate more manageable statistical distributions.<br>
It follows the recommendations of the authors in section 4.5.9.1 – Treatment of outliers, page 164.<br>
Here we will mask out the outliers by replacing these values by the NA R notation (Not Available)<br>

### Encoding Outliers values as NA

> wcs2train.ratios.NA <- wcs2train.ratios<br>
> for(i in 1:length(wcs2train.ratios.NA)){<br>
> \# use the function to identify extreme outliers<br>
> extreme.outl <- FindOutliers(wcs2train.ratios.NA[,i])<br>
> \# Replacing extreme outliers values by NA<br>
> wcs2train.ratios.NA[,i][extreme.outl] <- NA<br>
> cat(sprintf("%s\n", colnames(wcs2train.ratios)[i]))<br>
> }<br>

In order to graphically evaluate the effects of this ecoding we use the chart.Correlation() from the PerformanceAnalytics R package -> https://cran.r-project.org/web/packages/PerformanceAnalytics/index.html<br>

> library("PerformanceAnalytics")<br>
> chart.Correlation(wcs2train.ratios.NA, histogram=TRUE, pch=19)

The result is illustared in Table_4_21b_Page164_AllvariableswithNA_CoorDiag.pdf
<img src="./assets/Table_4_21b_Page164_AllvariableswithNA_CoorDiag.JPG" alt="drawing" width="100%"/>
