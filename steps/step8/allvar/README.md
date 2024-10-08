## Correlation study for all ratio variables (page 162)

The ratio variables span indexes 86 to 119 in the 7a) Testing on selected ratio variables (page 161) data table<br>
We are using the corrplot R package for display.<br
We are following the examples of: -> http://www.sthda.com/english/wiki/visualize-correlation-matrix-using-correlogram

> install.packages("corrplot")
> library(corrplot)
> corrprs	<- cor(wcs2train[,c(86:119)], use="pairwise", method="pearson")
> p.mat <- cor.pvalue(wcs2train[,c(86:119)])
> col <- colorRampPalette(c("#BB4444", "#fcc3b8", "#FFFFFF", "#add2f7", "#4fc69d"))
> corrplot(corrprs, method="color", col=col(200),  
         type="upper",<br> 
         addCoef.col = "black", \# Add coefficient of correlation<br>
         addCoefasPercent = TRUE,<br>
         tl.col="black", tl.srt=45, \# Text label color and rotation<br>
         \# Combine with significance
         p.mat = p.mat, sig.level = 0.01, insig = "blank",<br>
         \# hide correlation coefficient on the principal diagonal<br>
         diag=FALSE<br>
         )<br>

<em>NOTE:</em> Hexa ramp colors have been tuned using tool in Google Search.
The display blanks out the color of cells below significance level of 0.01 (1%), as indicated on page 160, last line.<br>

The graphics representation of the Pearson correlation between all Ratio Variables is presented in: Table_4_19b_Page 162_Ratios_Correlation.pdf
<img src="./assets/Table_4_19b_Page 162_Ratios_Correlation.JPG" alt="drawing" width="60%"/>

From this diagram, we detremine the following groups of correlated variables (over 70%).<br> 
<em>NOTE:</em> The groups are identical to those proposed in the author's text<br>

<strong>GR1: ROE, ROETR (Negative 73% with ROE), DEBTEQUTR (Negative 69% with ROETR and 51% with ROE)</strong><br>
| Column in R table  | Code in text | Description |
| ------------- | ------------- | ------------ |
| ROE-86		| ROE			| Ratio Net Profit/Equity 
| DEBTEQUTR-118	| DebtEquityTr	         | Ratio Interest-bearing Financial Debt/Equity 
| ROETR-119	| ROETr			| Ratio Net Profit/Total Stockholder's Equity 

<strong>GR2: EBITDAON, V89A (88% with EBITDAON), ROS (99% with EBITDAON)</strong><br>
| Column in R table  | Code in text | Description |
| ------------- | ------------- | ------------ |
| EBITDAON-87	| EBITDAonSALES	| Ratio EBITDA/Sales [%]
| V89A-90	| EBITDAonVP	| Ratio EBITDA/Value of Production
| ROS-91		| ROS	         | Ratio EBIT/Sales [%]

<strong>GR3: ROI, ASSETSTU (99% with ROI and ROA), ROA (100% with ROI), IEONLIAB (73% with ROAMINUS), ROAMINUS (100% with ROI and ROA and 99% with ASSETSTU)</strong><br>
| Column in R table  | Code in text | Description |
| ------------- | ------------- | ------------ |
| ROI-88		| ROI		| Ratio EBIT/Operating Assets [%]
| ASSETSTU-92	| ASSETS_TURNOVER	| Ratio Total Assets/Turnover
| ROA-89		| ROA		| Ratio Current Income/Total Assets [%]
| IEONLIAB-101	| IEonLIABLITIES	| Ratio Interest Expenses/Liabilities [%]
| ROAMINUS-115	| ROAminusIEonTL	| ROA minus Ratio Interest Expenses/Total Liabilities

<strong>GR4: V94A, V95A, COMMERCI (98% with V95A)</strong><br>
| Column in R table  | Code in text | Description |
| ------------- | ------------- | ------------ |
| V94A-95	| RECEIVABLES_PERIOD	| Ratio Trade Receivables/Daily Sales
| V95A-96	| INVENTORY_PERIOD	| Ratio Inventory/Daily Sales
| COMMERCI-98	| COMMERCIAL_WC_PERIOD	| Ratio (Trade Receivables + Inventory – Trade Payables)/Daily Sales

<strong>GR5: IEONEBIT, NIEONEBI (99%)</strong><br>
| Column in R table  | Code in text | Description |
| ------------- | ------------- | ------------ |
| IEONEBIT-99	| IEonEBITDA	| Ratio Interest Expenses/EBITDA [%]
| NIEONEBI-100	| NIEonEBITDA	| Ratio Net Interest Expenses/EBITDA [%]






