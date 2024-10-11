## Computing outliers percentage for all the ratios

We start by sub-setting the ratios from the W_CS_1_AnalysisSampleDataSet_2B.xls table

> ratiovars <- c(86:119)<br>
> wcs2train.ratios <- wcs2train[ratiovars]<r>
> sapply(wcs2train.ratios, class)<br>

The percentage of outliers is then computed for all the Ratio variables

> for(i in 1:length(wcs2train.ratios)){<br>
> \# use the function to identify extreme outliers<br>
> extreme.outl <- FindOutliers(wcs2train.ratios[,i])<br>
> \# compute percentage of extreme outliers<br>
> outlprc = length(extreme.outl)/length(wcs2train.ratios[,i])<br>
> cat(sprintf("%s, %.2f\n", colnames(wcs2train.ratios)[i], outlprc))<br>
> }<br>

 ##### <em>Highest outliers percentage:
| Ratio | Percentage | Ratio | Percentage | Ratio | Percentage | Ratio | Percentage |
| ----- | ---------- | ----- | -----------| ----- | ---------- | ----- | -----------|
| EXTRIC | 0.24 | SALESONV | 0.13 | ROE | 0.12 | INVENTOR | 0.1 |
</em>
<em>NOTE :</em> The results show that: <em>ROE, INVENTOR, EXTRIC</em> and <em>SALESONV</em> do have “outliers” percentage >= 10%

 ##### <em>Lower outliers percentage:
| Ratio | Percentage | Ratio | Percentage | Ratio | Percentage | Ratio | Percentage |
| ----- | ---------- | ----- | -----------| ----- | ---------- | ----- | -----------|
| DEBTEQU | 0.09 | EBITDAIE | 0.09 | RECEIVAB | 0.09 | ROETR | 0.09 | 
| DEBTEQUTR | 0.08 | SALESMIN | 0.07 | ROAMINUS | 0.06 | V95A | 0.06 |  
| EQUILIABL | 0.05 | EQUITYON | 0.05 | IEONEBIT | 0.05 | IEONFINA. | 0.05 |
| NIEONEBI | 0.05 | ROA | 0.05 | COMMERCI | 0.04 | CURRENT | 0.04 |
| PAYABLES | 0.04 | ROI | 0.04 | ROS | 0.04 | V89A | 0.03 |
| EBITDAON | 0.03 | QUICKRA | 0.02 | TAXESONG | 0.02 | ASSETSTU | 0.01 |
| V94A | 0.01 |    |    |    |    |    |    |
</em>
<em>NOTE :</em> It worth pointing out that a few NA (Not available) values are present, principaly in the <em>TAXESONG</em> ratio


 ##### <em>Anomalous outliers percentage:
| Ratio | Percentage | Ratio | Percentage | Ratio | Percentage | Ratio | Percentage |
| ----- | ---------- | ----- | -----------| ----- | ---------- | ----- | -----------|
| IEONLIAB | 0 | INTANGIB | 0 | TRADERE. | 0 | V110A | 0 |
| TRADEPA. | 0 |    |    |    |    |    |    |
</em>
<em>NOTE :</em> The results show anomalies in the computation of the quantiles for IEONLIAB, INTANGIB, TRADERE., V110A and TRADEPA:

- for IEONLIAB it is probably due to the presence of one extreme outlier (value 107.47) for a population ranging 0-23
- for all the other ratios the result is harder to explain



