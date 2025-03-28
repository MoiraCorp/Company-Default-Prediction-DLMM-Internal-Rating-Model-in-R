## Detecting LogNormal distributions and applying a Fisher transformation

We are here assessing the LogNormal nature of some of the distributions by using the so called Fisher Transform:<br>
z = 1/2 ln((1-r)/(1-r)) = arctanh(r)<br>
This transform meant to turn the distribution of a correlation coefficient r into a Normal Distribution.<br>
It needs the variable to be transformed into interval (-1, +1) before it is applied.

> \# 15 figures arranged in 3 rows and 5 columns
> j = 0
> my_plots = list()
> for(i in 1:15){ <br>
        j = j + 1 <br>
	x <- wcs2train.ratios.MON[,i] <br>
	minx <- min(x, na.rm=T) <br>
	maxx <- max(x, na.rm=T) <br>
	z <- (x - minx) / (maxx - minx) * 2 - 1 <br>
	at <- atanh(z) <br>
	y <- wcs2train$BADGOOD <br>
	d <- data.frame(at,y) <br>
	my_plots[[j]] <- qplot(at, data=d, geom="density", fill=y, alpha=I(.5),  <br>
   		main = sprintf("Density distribution of %s",names(wcs2train.ratios.MON)[i]), xlab="x",  <br>
  		ylab="Density") <br>
	cat(sprintf("Plot of %s\n", colnames(wcs2train.ratios.MON)[i])) <br>
} <br>
>  grid.arrange(grobs = my_plots, nrow = 3)
