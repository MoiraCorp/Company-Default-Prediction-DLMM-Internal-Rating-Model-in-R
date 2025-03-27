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

We decide to retrain the variables: INVENTOR, V95A and V110A after masking their exception values by recoding as NA
The variables: EXTRIC, TAXESONG and SALESONV are excluded from this study phase.

> wcs2train.ratios.MON <- wcs2train.ratios.NA
> wcs2train.ratios.MON[["INVENTOR"]] [ wcs2train.ratios.MON[["INVENTOR"]] == -1 ] <- NA
> wcs2train.ratios.MON[["V95A"]] [ wcs2train.ratios.MON[["V95A"]] == 0 ] <- NA
> wcs2train.ratios.MON[["V110A"]] [ wcs2train.ratios.MON[["V110A"]] == 0 ] <- NA

The isopopulation “binning” avoids processing EXTRIC, TAXESONG and SALESONV by use of a seq object (idem, list of indices)
It processe 31 variables.

> STATUS <- wcs2train$BADGOOD
> RATIO9vSTATUS <- cbind.data.frame(STATUS=levels(STATUS)[STATUS])
> varcount = 1
> seq <- c(1:17,20:27,29:34)
> for(i in seq){   <br>
	cat(sprintf("%s - %s\n", i, colnames(wcs2train.ratios.MON)[i]))  <br>	
	bins_cut = 9  <br>
	for(j in 1:bins_cut) {  <br>
		if(j == 1){  <br>
	        	collist <- c(sprintf("%s_1",names(wcs2train.ratios.MON)[i]))  <br>
		} else {  <br>
			collist <- append(collist, sprintf("%s_%s",names(wcs2train.ratios.MON)[i],j))  <br>
		}  <br>
	}  <br>
	ratio9 <- with(wcs2train.ratios.MON, bin.var(wcs2train.ratios.MON[,i], bins=bins_cut, method='proportions', labels=collist))  <br>
	RATIO9vSTATUS <- cbind.data.frame(RATIO9vSTATUS, ratio9=levels(ratio9)[ratio9])  <br>
	varcount = varcount + 1;  <br>
	names(RATIO9vSTATUS)[varcount] = names(wcs2train.ratios.MON)[i]  <br>
}  <br>
> ncol(RATIO9vSTATUS)
> [1] 32

This table has the variable STATUS in first column followed by the 31 “binned” variables. We finally generate out of this table presenting the default rates for 15 variables at time

> \# 15 figures arranged in 3 rows and 5 columns
> attach(mtcars)
> par(mfrow=c(3,5))
> for(i in 2:16){  <br>
	R9VB <- table(RATIO9vSTATUS[,i], RATIO9vSTATUS$STATUS)  <br>
	badrate <- R9VB[,1]/(R9VB[,1]+R9VB[,2])*100.0  <br>
	R9VB <- cbind(R9VB, badrate)  <br>
	plot(R9VB[,3], main = sprintf("Default rates for %s intervals",names(RATIO9vSTATUS)[i]), xlab = sprintf("%s(Binned)",names(RATIO9vSTATUS)[i]), ylab="Bad rate [%]")  <br>
	lines(R9VB[,3], type="b", pch=21, col="black", yaxt="n", lwd=2)  <br>
}  <br>

Default rates variation for variables: ROE,EBITDAON,ROI,ROA,V89A,ROS,ASSETSTU,INVENTOR,RECEIVAB,V94A,V95A,PAYABLES,COMMERCI,IEONEBIT,NIEONEBI (Table_4_26_Page 178_C2_Pt1.pdf)
<img src="./assets/Table_4_26_Page 178_C2_Pt1.jpg" alt="drawing" width="100%"/><br>

Default rates variation for variables: IEONLIAB,IEONFINA.,EXTRIC,TAXESONG,INTANGIB,TRADERE.,V110A,EQUITYON,TRADEPA.,DEBTEQU,CURRENT,QUICKRA,SALESONV,SALESMIN,ROAMINUS,EBITDAIE,EQUILIABL,DEBTEQUTR (Table_4_26_Page 178_C2_Pt2.pdf)
<img src="./assets/Table_4_26_Page 178_C2_Pt2.jpg" alt="drawing" width="100%"/><br>

Default rates variation for variable: ROETR (Table_4_26_Page 178_C2_Pt3.pdf)
<img src="./assets/Table_4_26_Page 178_C2_Pt3.jpg" alt="drawing" width="20%"/><br>

The results of evaluation are placed in the column “Empirical Monotinicity” from the synoptic table:  <a id="raw-url" href="https://github.com/MoiraCorp/DLMM-IRating-in-R/blob/main/steps/step11/relpro/assets/Ratios_Synoptic_De%20Laurentis.xls">Ratios_Synoptic_De Laurentis.xls</a>
Our evaluation is often in synch with that of the author.

Illustrated in: Ratios_Synoptic_De Laurentis.jpg
<img src="./assets/Ratios_Synoptic_De Laurentis.jpg" alt="drawing" width="100%"/>

