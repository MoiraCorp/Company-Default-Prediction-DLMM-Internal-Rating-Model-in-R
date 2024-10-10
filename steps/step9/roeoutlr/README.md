## Computing the number of outliers for the ration ROE (page 163)

Following the authors's approcah, we implement the FindOutliers() function in order to to detect extreme outliers

> FindOutliers <- function(data) {<br>
> lowerq = quantile(data, na.rm=TRUE)[2]<br>
> upperq = quantile(data, na.rm=TRUE)[4]<br>
> iqr = upperq - lowerq<br> 
> \# we identify extreme outliers<br>
> extreme.threshold.upper = (iqr * 3) + upperq<br>
> extreme.threshold.lower = lowerq - (iqr * 3)<br>
> result <- which(data > extreme.threshold.upper | data < extreme.threshold.lower)<br>
> }

More more information on the detection of outliers isn R, see: <br>
"Outliers detection in R" -> Outliers detection in R<br>

### The FindOutliers() function is used to evaluate the percentage of extereme outliers for the ROE variable

> extreme.outl <- FindOutliers(wcs2train$ROE)<br>
> \# compute percentage of extreme outliers<br>
> outlprc = length(extreme.outl)/length(wcs2train$ROE)<br>
> outlprc
 ##### <em>The printed output is:
 &nbsp;  [1] 0.1210692



