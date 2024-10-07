## Testing on selected ratio variables (page 161)

In order to illustrate the process (Table 4.19, pp 161), the authors have selected the following ratio variables:
- <strong>ROE-86</strong> = Ratio Net Profit/Equity
- <strong>IEONLIAB-101</strong> = Interest Expenses/Liabilities
- <strong>V110A-107</strong> = Inventories/Total Assets

  Using the cor() function from the standard R package:
> corrprs<- cor(wcs2train[,c(86,101,107)], use="pairwise", method="pearson")<br>
> corrprs<br>
