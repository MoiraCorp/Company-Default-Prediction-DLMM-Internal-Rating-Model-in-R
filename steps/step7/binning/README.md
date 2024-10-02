## Comparison between BADGOOD distribution and a binned ROE

The authors state that "empirical motonicity" between a (continuous or ordinal) variable X and the BADGOOD classes happens when we obtain a monotonic increase (or decrease) of default rates (idem, relative number of “Bad” companies) relatively to variable X categorized into continuous ordered intervals (idem, encoded as an ordinal variable)<br> 
In this case the comparison element is the average of default rates of borrowers included into variable X category intervals (idem, for example, the number of “Bad” companies in the interval divided by total number of these “Bad” companies)

<em>NOTE:</em> This "empirical motonicity" property tranlates into what is called a "Guttman Effect" in J. P. Benzécri Correspondence Analysis Theory (see: J-P Benzécri, Correspondence Analysis Handbook, Statistics: A Series of Textbooks and Monograph series, CRC Press, 1992, 688 pages, ISBN: 0824784375 or Blasius, J. (2011). Correspondence Analysis. In: Lovric, M. (eds) International Encyclopedia of Statistical Science. Springer, Berlin, Heidelberg. https://doi.org/10.1007/978-3-642-04898-2_195)<br>

### The binning function bin.var()
We are binning the ROE variable in 9 (10 boundaries) equally populated bins using the special purpose bin.var () function developed in R<br>
> bin.var <- function (x, bins = 4, method = c("intervals", "proportions",
    "natural"), labels = FALSE)<br>
= {<br>
    method <- match.arg(method)<br>
    if (length(x) < bins) {
        stop("The number of bins exceeds the number of data values")
    }<br>
    x <- if (method == "intervals") 
        cut(x, bins, labels = labels)<br>
    else if (method == "proportions") 
        cut(x, quantile(x, probs = seq(0, 1, 1/bins), na.rm = TRUE), 
            include.lowest = TRUE, labels = labels)<br>
    else {
        xx <- na.omit(x)
        breaks <- c(-Inf, tapply(xx, KMeans(xx, bins)$cluster, 
            max))<br
        cut(x, breaks, labels = labels)<br>
    }<br>
    as.factor(x)<br>
}<br>

### Building an encoded ROE into 9 equal-population intervals (10 boundaries)

#### Listing the boundaries of the encoding
> bins_cut = 9<br>
> quant <- quantile(wcs2train$ROE, probs = seq(0, 1, 1/bins_cut), na.rm = TRUE)<br>
> quant<br>
##### <em>The printed output is:
&nbsp;           0%    11.11111%    22.22222%    33.33333%    44.44444%    55.55556%    66.66667%    77.77778%    88.88889%         100%<br>
&nbsp; -5500.000000   -47.512000    -5.779667     1.370000     5.747778    13.950778    25.828667    48.020222   100.000000 17930.000000</em><br>

#### Encoding ROE as a factor
> bins_cut = 9<br>
> for(j in 1:bins_cut) {<br>
	if(j == 1){
		collist <- c(sprintf("%s_1","ROE"))<br>
	} else {
		collist <- append(collist, sprintf("%s_%s","ROE",j))
	}<br>
}<br>
> ROE9 <- with(wcs2train, bin.var(wcs2train$ROE, bins=bins_cut, method='proportions', labels=collist))<br>
> table(ROE9, wcs2train$BADGOOD)<br>
 ##### <em>The printed output is:      
&nbsp; ROE9    "Bad" "Good"<br>
&nbsp;   ROE_1     6    136<br>
&nbsp;   ROE_2    13    128<br>
&nbsp;   ROE_3     9    133<br>
&nbsp;   ROE_4     4    136<br>
&nbsp;   ROE_5     2    139<br>
&nbsp;   ROE_6     5    136<br>
&nbsp;   ROE_7     3    138<br>
&nbsp;   ROE_8     2    141<br>
&nbsp;   ROE_9     7    133<br>

#### Graphing the binned ROE
> plot(ROE9VB[,1], main = "Fig 4.17 - Default rates for ROE intervals", xlab="ROE(Binned)", ylab="Mean Bad/ROE interval")<br>
> lines(ROE9VB[,1], lwd=2)<br>

The resulting graph is presented in  : Fig_4_17_Page 158_ROEBin_Bad.pdf
<img src="./assets/Fig_4_17_Page 158_ROEBin_Bad.JPG" alt="drawing" width="50%"/>

