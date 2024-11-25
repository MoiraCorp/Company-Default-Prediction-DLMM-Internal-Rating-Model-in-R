## Transformation of indicators using a logistic formula: the case of the ROE ratio

Many of the accounting variables as well their Ratios display a form of LogNormal distribution. This is often encountered form in the statistical distribution of “quantities” either in nature or in the social sciences.<br>
The logistic formula offers a way to transform the variables so that their distribution is closer to a Normal distribution. As it applies a Log transform, it is also another way to reduce the influence of “extreme” values (idem, “extreme” outliers)In SPPS, the CDF.LOGISTIC function can be used for the perform a LogNormal to Normal distribution transformation (-> https://www.ibm.com/docs/en/spss-statistics/beta?topic=functions-cumulative-distribution)</p>
In SPPS, the CDF.LOGISTIC function can be used for the perform a LogNormal to Normal distribution transformation (-> https://www.ibm.com/docs/en/spss-statistics/beta?topic=functions-cumulative-distribution)<br>
It is call as: CDF.LOGISTIC(quant, mean, scale) and returns the cumulative probability that a value from the logistic distribution, with the specified mean and scale parameters, will be less than quant.<br>
This corresponds to the mathematical formula: y = 1/(1+e**-(x-a)/b)) with a = mean and b = scale</p>

We have programmed this function in R as CDFlogistic()<br>
> CDFlogistic <- function(x,a,b){<br>
>   power <- (x-a)/b<br>
>   transform <- 1 / (1 + exp(-power))<br>
>   return(transform)<br>
> }
>

We follow by performing the logistic transformation recommanded by the authors (pp 170).<br>
However, in order to get an histogram similar to that of presented on page 169, the recommanded slope of 1500 in the book needs to be divided by 10 in our case.<br>
> logit <- CDFlogistic(wcs2train$ROE,0,150)<br>
> hist(logit, breaks = 50)<br>
> LOGIT_ROE <- data.frame(logit)<br>

It is followed by the necessary R calls in order to produce a comparative display of the ROE distribution before and after logistic transformation <br>

Apart from the ggplot2 package, we use the ggplotr R display package (an extension to ggplot2) (-> https://cran.r-project.org/web/packages/qqplotr/index.html and https://cran.r-project.org/web/packages/qqplotr/vignettes/introduction.html) as well as the gridExtra R package for extar grid graphics capability (-> https://cran.r-project.org/web/packages/gridExtra/index.html )<br>

> library(ggplot2)<br>
> install.packages("qqplotr")<br>
> library("qqplotr")<br>
> install.packages("gridExtra")<br>
> library("gridExtra")<br>
> p1 <- ggplot(data=wcs2train, mapping = aes(sample=ROE)) + stat_qq_line (color="grey") + stat_qq_point(color="light blue") + labs(x = "Normal Quantiles", y = "Observed Interest Expenses/Liabilities(ROE) Quantiles")<br>
> p1 <- p1 + scale_y_continuous(limits=c(-2000,2000), breaks=seq(-2000,2000,500), expand = c(0, 0))<br>
> p2 <- ggplot(data=LOGIT_ROE, mapping = aes(sample=logit)) + stat_qq_line (color="grey") + stat_qq_point(color="orange") + labs(x = "Normal Quantiles", y = "Logit transformed (ROE) Quantiles")<br>
> p2 <- p2 + scale_y_continuous(limits=c(0,1), breaks=seq(0,1,0.25), expand = c(0, 0))<br>
> p3 <- qplot(ROE, data=wcs2train, fill=I("light blue"), col=I("black")) + ggtitle("Interest Expenses/Liabilities (ROE)")<br>
> p4 <- qplot(logit, data=LOGIT_ROE, fill=I("orange"), col=I("black")) + ggtitle("Logit transformed (ROE)")<br>
> grid.arrange(p3, p4, p1, p2, nrow = 2)<br>
