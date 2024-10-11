## Computing outliers percentage for all the ratios

We start by sub-setting the ratios from the W_CS_1_AnalysisSampleDataSet_2B.xls table

> ratiovars <- c(86:119)<br>
> wcs2train.ratios <- wcs2train[ratiovars]<r>
> sapply(wcs2train.ratios, class)<br>

The percentage of outliers is then computed for all the Raio variables

> for(i in 1:length(wcs2train.ratios)){<br>
> \# use the function to identify extreme outliers<br>
> extreme.outl <- FindOutliers(wcs2train.ratios[,i])<br>
> \# compute percentage of extreme outliers<br>
> outlprc = length(extreme.outl)/length(wcs2train.ratios[,i])<br>
> cat(sprintf("%s, %.2f\n", colnames(wcs2train.ratios)[i], outlprc))<br>
> }<br>

 ##### <em>The printed output is:
| Ratio | Percentage | Ratio | Percentage | Ratio | Percentage | Ratio | Percentage |
| ----- | ---------- | ----- | -----------| ----- | ---------- | ----- | -----------|
| EXTRIC | 0.24 | SALESONV | 0.13 | ROE | 0.12 | INVENTOR | 0.1 |
</em>

 ##### <em>The printed output is:
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

 ##### <em>The printed output is:
| Ratio | Percentage | Ratio | Percentage |
| ----- | ---------- | ----- | -----------|
| EBITDAON | 0.03 | IEONFINA. | 0.05 |
| ROI | 0.04 | TAXESONG | 0.02 |
| ROA | 0.05 | EQUITYON | 0.05 |
| V89A | 0.03 | DEBTEQU | 0.09 |
| ROS | 0.04 | CURRENT | 0.04 |
| ASSETSTU | 0.01 | QUICKRA | 0.02 |
| RECEIVAB | 0.09 | SALESMIN | 0.07 |
| V94A | 0.01 | ROAMINUS | 0.06 |
| V95A | 0.06 | EBITDAIE | 0.09 |
| PAYABLES | 0.04 | EQUILIABL | 0.05 |
| COMMERCI | 0.04 | DEBTEQUTR | 0.08 |
| IEONEBIT | 0.05 | ROETR | 0.09 |
| NIEONEBI | 0.05 |  |  |
</em>

 ##### <em>The printed output is:
| Ratio | Percentage | Ratio | Percentage |
| ----- | ---------- | ----- | -----------|
| IEONLIAB | 0 | INTANGIB | 0 |
| TRADERE. | 0 | V110A | 0 |
| TRADEPA. | 0 |  |  |




