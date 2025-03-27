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

Some variables are not amenable to “Binning” by the bin.var() function (with index going from 1:34):

- 8 - INVENTOR	-> This variable has 154 values = -1
- 11 - V95A	-> This variable is equal to INVENTOR/SALES, has 154 corresponding values = 0	
- 18 - EXTRIC	-> This variable should probably be excluded from this process. It has 502 values = 1 which are either convential values or excessive rounding operation results.
- 19 - TAXESONG	-> This variable should probably excluded from this process. It is a similar case than EXTRIC. It has 305 values = 0 and 5 values = NA (A rare case in this datatable)
- 22 - V110A	-> This variable is equal to INVENTOR/TOTAL ASSETS and  has 154 corresponding values = 0
- 28 – SALESONV	-> This variable should probably be excluded from this process. Its is equal to SALES/Value of production (or OPRE), and has 517 values = 100
