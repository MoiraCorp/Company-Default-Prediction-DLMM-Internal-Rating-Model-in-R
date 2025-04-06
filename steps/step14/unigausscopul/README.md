## Testing GOOD-BAD separability with Uniform and Gaussian Copula encoding

We are testing the effect of the Gauss Copula encoding on the separability between BAD and GOOD groups for the ROE ratio.

> library(ggplot2) <br>
> library("gridExtra") <br>
> my_plots = list() <br>
> \# 3 figures arranged in 1 rows and 3 columns <br>
> 	x <- wcs2train$ROE <br>
> 	y <- wcs2train$BADGOOD <br>
> 	d <- data.frame(x,y) <br>
> 	my_plots[[1]] <- qplot(x, data=d, geom="density", fill=y, alpha=I(.5),  <br>
   		main = sprintf("Density distribution of ROE"), xlab="x",  <br>
  		ylab="Density") <br>
> 	x <- ROE256 <br>
> 	y <- wcs2train$BADGOOD <br>
> 	d <- data.frame(x,y) <br>
> 	my_plots[[2]] <- qplot(x, data=d, geom="density", fill=y, alpha=I(.5),  <br>
   		main = sprintf("Density distribution of ROE Encoded Isopopulation"), xlab="x",  <br>
  		ylab="Density") <br>
> 	x <- ROE256G <br>
> 	y <- wcs2train$BADGOOD <br>
> 	d <- data.frame(x,y) <br>
> 	my_plots[[3]] <- qplot(x, data=d, geom="density", fill=y, alpha=I(.5),  <br>
   		main = sprintf("Density distribution of ROE Encoded Gauss"), xlab="x",  <br>
  		ylab="Density") <br>
> grid.arrange(grobs = my_plots, nrow = 1) <br>
