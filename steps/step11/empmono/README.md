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
