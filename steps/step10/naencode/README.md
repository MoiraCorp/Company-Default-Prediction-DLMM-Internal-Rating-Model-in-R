## Replacement of NA encoded outliers by multidimensional interpolation

In the previous section (step9), we have detected “extreme outliers” and encoded them as NA (not Available)<br>
However, most AI methods require the processing FULL datatables.<br>

In sction 4.5.9.1 Treatment of outliers and shapes of distributions (pp 164-165), the authors propose to “fill in” the masqued outliers with either the mean or the median of each of the Ratio Variable statistical distribution.<br>
Although it is common practice, <em>this method is based on a very thin probability theory argument</em>.<br><br>

The present dataset being essentially “multidimensional” it is better justified to proceed with the replacement of the NA values on the basis of the multidimensional relations existing between the Ratio Variables rather than processing them individually. In our case, all variables being numerical (see list below), we will apply Principal Componant Analysis (PCA) and follow by an "interpolation" of the missong valeus based on the PCA factor space vectors. This is performed using the missMDA R package (-> https://cran.r-project.org/web/packages/missMDA/index.html) following a PCA detremined using the FactoMineR R package (-> https://cran.r-project.org/web/packages/FactoMineR/index.html)

> \# Checking on variables type in the datatable<br>
> sapply(wcs2train.ratios.NA, class)<br>





### Comparison of Ratio Variables range and statistics before and after “outliers” processing

### Study of Ratio Variables correlation properties after “outliers” processing
