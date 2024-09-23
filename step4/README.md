# Exploring the probability distribution of each variable

It follows the section: 4.5.4 Graphical analysis (page 140 of the DLMM book)<br>
We want to uses Box plots, Q–Q plots graphical displays
in order to visualise the outliers of each distribution (Box plot) <br>
and test the normality of each of these distributions distribution (Q-Q plot)  <br><br>

#### Using the standard plot() function
Although it is always possible to get a quick display of a variable ditrbution using the standard R plot() function such as in the following:
> plot(wcs2train$ROE~wcs2train$BADGOOD, xlab="Status", ylab="ROE", main="Boxplots of ROE by Status")

As the range of the variable distribution is hugely, this display is poor it is preferable to use more appropriate functions<br>

#### Using ggplot() Box plot function for the display of ROE (Ratio Net Profit/Equity)
Far more useful displays are generated using the Box plot ggplot() from the ggplot2 R package
> library(ggplot2)<br>
> ggplot(wcs2train, aes(x = wcs2train$BADGOOD, y = wcs2train$ROE)) + stat_boxplot(geom ='errorbar', width=0.1) + geom_boxplot(width=0.2, fill='#A4A4A4') + 
	labs(x = "01STATUS",y = "Netprofit/Equity") + scale_y_continuous(limits=c(-300,300), breaks=seq(-300,300,100), expand = c(0, 0))<br>

<em>NOTE:</em> Here we have accumulated a few tricks using ggplot in ggplot2 package
- stat_boxplot(geom ='errorbar', width=0.1) give whiskers with a controlled width
- labs(x = "01STATUS",y = "Netprofit/Equity") controls the legend x/y
- geom_boxplot(width=0.2, fill='#A4A4A4') slects a gray color for the boxes witha controlled width
- scale_y_continuous(limits=c(-300,300), breaks=seq(-300,300,100), expand = c(0, 0)) set the y axis upper and lower values while selecting the break ticks


