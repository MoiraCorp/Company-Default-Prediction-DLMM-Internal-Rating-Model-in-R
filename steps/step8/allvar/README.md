## Correlation study for all ratio variables (page 162)

The ratio variables span indexes 86 to 119 in the 7a) Testing on selected ratio variables (page 161) data table<br>
We are using the corrplot R package for display.<br
We are following the examples of: -> http://www.sthda.com/english/wiki/visualize-correlation-matrix-using-correlogram

> install.packages("corrplot")
> library(corrplot)
> corrprs	<- cor(wcs2train[,c(86:119)], use="pairwise", method="pearson")
> p.mat <- cor.pvalue(wcs2train[,c(86:119)])
> col <- colorRampPalette(c("#BB4444", "#fcc3b8", "#FFFFFF", "#add2f7", "#4fc69d"))
> corrplot(corrprs, method="color", col=col(200),  
         type="upper",<br> 
         addCoef.col = "black", \# Add coefficient of correlation<br>
         addCoefasPercent = TRUE,<br>
         tl.col="black", tl.srt=45, \# Text label color and rotation<br>
         \# Combine with significance
         p.mat = p.mat, sig.level = 0.01, insig = "blank",<br>
         \# hide correlation coefficient on the principal diagonal<br>
         diag=FALSE<br>
         )<br>

>em>NOTE:</em> Hexa ramp colors have been tuned using tool in Google Search.
The display blanks out the color of cells below significance level of 0.01 (1%), as indicated on page 160, last line.<br>

The graphics representation of the Pearson correlation between all Ratio Variables is presented in: Table_4_19b_Page 162_Ratios_Correlation.pdf
