## Binning quantitative variables: the case of liaison between SALES and STATUS (BADGOOD) variables

A ROC analysis of the relation between SALES and Good-Bad status gives poor results similar to those obtained  with ROE,
the author has a similar opinion on page 173.

> library(pROC)<br>
> sales <- wcs2train$SALES<br>
> rocs = roc(wcs2train$BADGOOD, sales)<br>
> auc1 <- auc(rocs)<br>
##### <em>The printed output is:
Area under the curve: 0.5977
</em>
> roc1 = roc(wcs2train$BADGOOD, wcs2train$ROE)<br>
> \# Printing the ROC asymptotic intervals<br>
> ci1 <- ci(rocs)<br>
##### <em>The printed output is:
95% CI: 0.5213-0.674 (DeLong)
</em>
> \# Getting the Std. Error under a non parametric assumption<br>
> vr1 <- var(rocs)^0.5<br>
##### <em>The printed output is:
[1] 0.0389407
</em>

### Isopopulation «binning» of Log10-SALES in order to explore concordances of SALES level with default rate

### Using empirical « binning » proposed by authors on SALES in order to explore concordances of SALES level with default rate
