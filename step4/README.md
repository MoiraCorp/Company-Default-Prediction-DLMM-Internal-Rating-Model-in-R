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

<img src="Fig_4_10_Page 142_ROE_Box Plot_woutlabels.JPG" alt="drawing" width="60%"/>
<em>NOTE:</em> Here we have accumulated a few tricks using ggplot in ggplot2 package
- stat_boxplot(geom ='errorbar', width=0.1) give whiskers with a controlled width
- labs(x = "01STATUS",y = "Netprofit/Equity") controls the legend x/y
- geom_boxplot(width=0.2, fill='#A4A4A4') slects a gray color for the boxes witha controlled width
- scale_y_continuous(limits=c(-300,300), breaks=seq(-300,300,100), expand = c(0, 0)) set the y axis upper and lower values while selecting the break ticks

#### Using dplyr to label the outliers
Although the previous dispaly does separate the outliers from the 2-sigma range, the corresponding companies are not identified<br>
This done in this phase by creating the specific function is_outlier() built using the Rccp R package
> library(Rcpp)<br>
> library(dplyr)<br>
> library(ggplot2)<br>
> is_outlier <- function(x) {
  return(x < quantile(x, 0.25) - 1.5 * IQR(x) | x > quantile(x, 0.75) + 1.5 * IQR(x))
}<br>	
> wcs2train %>%
  group_by(BADGOOD) %>%
  mutate(outlier = ifelse(is_outlier(ROE), BORCODE, as.numeric(NA))) %>%
  ggplot(., aes(x = BADGOOD, y = ROE)) +
    stat_boxplot(geom ='errorbar', width=0.1) + geom_boxplot(width=0.2, fill='#A4A4A4') + 
    labs(x = "01STATUS",y = "Netprofit/Equity") + scale_y_continuous(limits=c(-300,300), breaks=seq(-300,300,100), expand = c(0, 0)) +
    geom_text(aes(label = outlier), na.rm = TRUE, hjust = -0.3, check_overlap = T)<br>

<img src="Fig_4_10_Page 142_ROE_Box Plot_withlabels.JPG" alt="drawing" width="60%"/>
<em>NOTE:</em> The dplyr package (as the magrittr package) use the %>% pipe operator
- the use of the mutate() function in order to build an outlier mask for the outliers is probably due to the use of mutate()
- the is-outlier() function labels the outliers
- geom_text(aes(label = outlier), na.rm = TRUE, hjust = -0.3, check_overlap = T) does the labelling of these points

#### Using ggrepel to identify the outliers
Although the outliers are labelled in the previous display they still are difficult to identify when they are closely clustered<br>
as they are all plotted on the same side of the axis<br>
In order to ease this individual identification, the use the ggrepel R package
> library(ggrepel)<br>
> library(dplyr)<br>
> library(ggplot2)<br>
> wcs2train %>%
  group_by(BADGOOD) %>%
  mutate(outlier = ifelse(is_outlier(ROE), BORCODE, as.numeric(NA))) %>%
  ggplot(., aes(x = BADGOOD, y = ROE)) +
    geom_boxplot() +
    scale_y_continuous(limits=c(-300,300), breaks=seq(-300,300,100), expand = c(0, 0)) +
    geom_text_repel(aes(label = outlier))<br>
> wcs2train %>%
  group_by(BADGOOD) %>%
  mutate(outlier = ifelse(is_outlier(ROE), BORCODE, as.numeric(NA))) %>%
  ggplot(., aes(x = BADGOOD, y = ROE)) +
    stat_boxplot(geom ='errorbar', width=0.1) + geom_boxplot(width=0.2, fill='#A4A4A4') + 
    labs(x = "01STATUS",y = "Netprofit/Equity") + scale_y_continuous(limits=c(-300,300), breaks=seq(-300,300,100), expand = c(0, 0)) +
    geom_text_repel(aes(label = outlier))<br>

<img src="Fig_4_10_Page 142_ROE_Box Plot_IDlabels.JPG" alt="drawing" width="80%"/>
<em>NOTE:</em> The ggrepel package is an extension of dplyr+ggplot2
- geom_text_repel replaces the geom_text function and enables to create pointers to outliers while avoiding the overlapping of labels.
Any outlier can thus be identified

