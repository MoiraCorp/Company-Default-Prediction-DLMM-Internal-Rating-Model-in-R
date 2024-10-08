## Testing on selected ratio variables (page 161)

In order to illustrate the process (Table 4.19, pp 161), the authors have selected the following ratio variables:
- <strong>ROE-86</strong> = Ratio Net Profit/Equity
- <strong>IEONLIAB-101</strong> = Interest Expenses/Liabilities
- <strong>V110A-107</strong> = Inventories/Total Assets

  Using the cor() function from the standard R package:
> corrprs<- cor(wcs2train[,c(86,101,107)], use="pairwise", method="pearson")<br>
> corrprs<br>
 ##### <em>The printed output is: 
|           | ROE    | IEONLIAB       | V110A| 
| --------- | ------- | ------------ |--------- |
| ROE        |  1.00000000  | -0.02538354  | -0.03441025
| IEONLIAB   | -0.02538354  | 1.00000000   | -0.03018398
| V110A      | -0.03441025  | -0.03018398  | 1.00000000
</em>

In order to compute the matrix of p-value, the custom cor.pvalue() R function is used  following: -> http://www.sthda.com/english/wiki/visualize-correlation-matrix-using-correlogram<br>

> cor.pvalue <- function(mat, ...) {<br> 
    mat <- as.matrix(mat)<br>
    n <- ncol(mat)<br>
    p.mat<- matrix(NA, n, n)<br>
    diag(p.mat) <- 0<br>
    for (i in 1:(n - 1)) {<br>
        for (j in (i + 1):n) {<br>
            tmp <- cor.test(mat[, i], mat[, j], ...)<br>
            p.mat[i, j] <- p.mat[j, i] <- tmp$p.value<br>
        }<br>
    }<br>
  colnames(p.mat) <- rownames(p.mat) <- colnames(mat)<br>
  p.mat
}<br>

> \# matrix of the p-value of the correlation<br>
> p.mat<- cor.pvalue (wcs2train[,c(86,101,107)])<br>
> p.mat<br>
 ##### <em>The printed output is: 
|           | ROE    | IEONLIAB       | V110A| 
| --------- | ------- | ------------ |--------- |
| ROE      | 0.0000000 | 0.3656972 | 0.2200474
| IEONLIAB | 0.3656972 | 0.0000000 | 0.2820608
| V110A    | 0.2200474 | 0.2820608 | 0.0000000
</em>
<em>NOTE :</em> The values of correlation and p-value are combined in one table on page 161

> corrspm<- cor(wcs2train[,c(86,101,107)], use="pairwise", method="spearman")
> corrspm <br>
 ##### <em>The printed output is: 
|           | ROE    | IEONLIAB       | V110A| 
| --------- | ------- | ------------ |--------- |
| ROE      | 1.00000000   | -0.15264427 | -0.05102912
| IEONLIAB | -0.15264427  | 1.00000000  |  0.02129009
| V110A    | -0.05102912  | 0.02129009  |  1.00000000
</em>

In supplement, the R cor() function offers the Kendall parametric correlation 

> corrken<- cor(wcs2train[,c(86,101,107)], use="pairwise", method="kendall")
> corrken<br>
 ##### <em>The printed output is: 
|           | ROE    | IEONLIAB       | V110A| 
| --------- | ------- | ------------ |--------- |
| ROE      | 1.0000000   | -0.10461972 | -0.03484200
| IEONLIAB | -0.1046197  | 1.00000000  |  0.01552111
| V110A    | -0.0348420  | 0.01552111  |  1.00000000
</em>








 
