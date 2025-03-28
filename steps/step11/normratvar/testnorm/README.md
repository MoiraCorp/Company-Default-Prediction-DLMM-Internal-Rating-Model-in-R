## Characterizing the form of the Ratio Variables distributions

We compute the histogram or each of the ratios (function: dnesity()) and present them  for 15 variables at time

> \# 15 figures arranged in 3 rows and 5 columns
> attach(mtcars)
> par(mfrow=c(3,5))
> for(i in 1:15){ <br>
plot(density(wcs2train.ratios.MON[,i], na.rm=TRUE),  <br>
	main = sprintf("Density distribution of %s",names(wcs2train.ratios.MON)[i]),  <br>
	xlab = sprintf("Values of %s",names(wcs2train.ratios.MON)[i]), ylab="Density Probability") <br>
} <br>

> library(ggplot2)
> library("gridExtra")
> j = 0
> my_plots = list()
> \# 15 figures arranged in 3 rows and 5 columns
> for(i in 1:15){ <br>
        j = j + 1 <br>
	x <- wcs2train.ratios.MON[,i] <br>
	y <- wcs2train$BADGOOD <br>
	d <- data.frame(x,y) <br>
	my_plots[[j]] <- qplot(x, data=d, geom="density", fill=y, alpha=I(.5),  <br>
   		main = sprintf("Density distribution of %s",names(wcs2train.ratios.MON)[i]), xlab="x",  <br>
  		ylab="Density") <br>
	cat(sprintf("Plot of %s\n", colnames(wcs2train.ratios.MON)[i])) <br>
} <br>
> grid.arrange(grobs = my_plots, nrow = 3)
