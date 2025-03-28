## Detecting LogNormal distributions and applying a Fisher transformation

We are here assessing the LogNormal nature of some of the distributions by using the so called Fisher Transform:<br>
z = 1/2 ln((1-r)/(1-r)) = arctanh(r)<br>
This transform meant to turn the distribution of a correlation coefficient r into a Normal Distribution.<br>
It needs the variable to be transformed into interval (-1, +1) before it is applied.

From previous step output (see -> Characterizing the form of the Ratio Variables distributions) it has beenestablished that  LogNormal distributed Ratio Variables are : ASSETSTU, INVENTOR, V95A, IEONLIAB, IEONFINA­, INTANGIB, V110A, DEBTEQUTR<br>
Their indexes in the wcs2train.ratios.MON datatable are: 7,8,11,16,17,20,22,33

Comparison of density shapes before and after the Fisher Transform being applied to these ratios is presented in a presented in a combined garphics document.

> \# 16 figures arranged in 4 rows and 4 columns
> j = 0
> my_plots = list()
> seq <- c(7,8,11,16,17,20,22,33)
for(i in seq){ <br>
        j = j + 1 <br>
	x <- wcs2train.ratios.MON[,i] <br>
	y <- wcs2train$BADGOOD <br>
	d <- data.frame(x,y) <br>
	my_plots[[j]] <- qplot(x, data=d, geom="density", fill=y, alpha=I(.5),  <br>
   		main = sprintf("Untransformed Density distribution of %s",names(wcs2train.ratios.MON)[i]), xlab="x",  <br>
  		ylab="Density") <br>
        j = j + 1 <br>
	x <- wcs2train.ratios.MON[,i] <br>
	minx <- min(x, na.rm=T) <br>
	maxx <- max(x, na.rm=T) <br>
	z <- (x - minx) / (maxx - minx) * 2 - 1 <br>
	at <- atanh(z) <br>
	y <- wcs2train$BADGOOD <br>
	d <- data.frame(at,y) <br>
	my_plots[[j]] <- qplot(at, data=d, geom="density", fill=y, alpha=I(.5),  <br>
   		main = sprintf("Fisher Transformed Density distribution of %s",names(wcs2train.ratios.MON)[i]), xlab="x",  <br>
  		ylab="Density") <br>
	cat(sprintf("Plot of %s\n", colnames(wcs2train.ratios.MON)[i])) <br>
} <br>
> grid.arrange(grobs = my_plots, nrow = 4)

Comparison between density shapes before-after Fisher Transform for ratios: (Table_4_26_Page 178_C6b_AllLogNorm.pdf)
<img src="./assets/Table_4_26_Page 178_C6b_AllLogNorm.jpg" alt="drawing" width="100%"/><br>

Overall, most of these variables show **a LOW DEGREE OF SEPARABILITY between GOOD and BAD** (idem, Default) groups

