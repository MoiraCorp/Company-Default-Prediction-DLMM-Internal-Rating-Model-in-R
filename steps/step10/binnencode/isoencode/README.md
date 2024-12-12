## Isopopulation «binning» of Log10-SALES in order to explore concordances of SALES level with default rate

Here we use an “isopupulation” binning method similar to the one already used in order to study the monotonicity of the Ratio Variables,
a technique already used in with function bin.var() section Step7-Binning (--> https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step7/binning). However, due to the strong LogNormal nature of the SALES probability distribution we will prefer to work with the Log10 of SALES rather than with the original values.

> logsales <- log10(wcs2train$SALES)<br>
> \# Cleaning: turning infinite values into NA<br>
> logsales[is.infinite(logsales)] = NA<br>
> LOGSALES <- data.frame(logsales)<br>
> library(ggplot2)<br>
> library("qqplotr")<br>
> library("gridExtra")<br>
> p1 <- qplot(SALES, data=wcs2train, fill=I("light blue"), col=I("black")) + ggtitle("SALES")<br>
> p2 <- qplot(logsales, data=LOGSALES, fill=I("orange"), col=I("black")) + ggtitle("Log10 of SALES")<br>
> grid.arrange(p1, p2, nrow = 1)<br>

The result is illustrated in: Fig_4_21b_Page 174_SALES_Log10.pdf
<img src="./assets/Fig_4_21b_Page 174_SALES_Log10.JPG" alt="drawing" width="80%"/>

In order to match the intervals proposed by the author we decides to section into 5 equipopulation “bins” which are determined using the quantile() function from the satndard R package.<b>

> bins_cut = 5<br>
> quant <- quantile(logsales, probs = seq(0, 1, 1/bins_cut), na.rm = TRUE)<br>
> quant<br>

##### <em>The printed output is:</b>
  Percent   0%   20%   40%    60%   80%   100%  
  Boundary   1.000   658.000   1403.195   2829.598   7591.993   464186.000 
</em>

<em>NOTE:</em> It is worth noting here that Log10-SALES vector has been previously “cleaned” the eliminating the minus-infinity values and replacing them by NA. Thus in SALES the firms with zero values have been discarded. This explains that here the minimum value is 1.


