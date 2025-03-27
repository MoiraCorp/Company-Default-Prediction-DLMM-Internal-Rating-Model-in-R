## Empirical Monotonicity determination

We are using the bin.var() function for isopopulation “binning”

> \# Loading the bin.var function for encoding continuous variables
> bin.var <- function (x, bins = 4, method = c("intervals", "proportions", <br>
    "natural"), labels = FALSE)  <br>
 {  <br>
    method <- match.arg(method)  <br>
    if (length(x) < bins) {  <br>
        stop("The number of bins exceeds the number of data values")  <br>
    }  <br>
    x <- if (method == "intervals")  <br>
        cut(x, bins, labels = labels)  <br>
    else if (method == "proportions")  <br>
        cut(x, quantile(x, probs = seq(0, 1, 1/bins), na.rm = TRUE),  <br>
            include.lowest = TRUE, labels = labels)  <br>
    else {  <br>
        xx <- na.omit(x)  <br>
        breaks <- c(-Inf, tapply(xx, KMeans(xx, bins)$cluster,  <br>
            max))  <br>
        cut(x, breaks, labels = labels)  <br>
    }  <br>
    as.factor(x)  <br>
}  <br>

We also decide to process the distributions after removal of “extreme” outliers in order to avoid spurious relations
And, we will not correct these values by interpolation.

> wcs2train.ratios.NA <- wcs2train.ratios  <br>
for(i in 1:length(wcs2train.ratios.NA)){  <br>
	\# use the function to identify extreme outliers  <br>
	extreme.outl <- FindOutliers(wcs2train.ratios.NA[,i])  <br>
> \# Replacing extreme outliers values by NA  <br>
	wcs2train.ratios.NA[,i][extreme.outl] <- NA  <br>
	cat(sprintf("%s\n", colnames(wcs2train.ratios)[i]))  <br>
}  <br>
