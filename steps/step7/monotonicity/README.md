## Developing a var/BADGOOD monotonicity detection scheme

#### Testing MCA for detecting monotonicity

Building a data.frame ROE9vSTATUS containing the cross-table between the binned ROE9 variable (ROE binned in 9 levels) versus STATUS variable <br>
It needs to use the bin.var() function which R code has neen introduced in this exrecise in the section: step7-binning<br>
and the R FactoMineR package -> https://cran.r-project.org/web/packages/FactoMineR/index.html<br>

> library(FactoMineR)
> ROE9 <- with(wcs2train, bin.var(wcs2train$ROE, bins=bins_cut, method='proportions', labels=collist))
> STATUS <- wcs2train$BADGOOD<br>
> ROE9vSTATUS <- cbind(ROE9=levels(ROE9)[ROE9], STATUS=levels(STATUS)[STATUS])
> summary(ROE9vSTATUS)

##### <em>The printed output is:
  ROE9   STATUS    
  ROE_8  :143  "Bad" :  51  
  ROE_1  :142  "Good":1220  
  ROE_3  :142                
  ROE_2  :141                
  ROE_5  :141                
  ROE_6  :141                
  (Other):421
</em>

We  then run the MCA (Multiple Correspondence Analysis) on the cross-table and list the factors scores on the first component
> ROE9vSTATUS.res<-MCA(ROE9vSTATUS, ncp=2, graph = TRUE)
> summary(ROE9vSTATUS.res)

##### <em>The printed output is:
Categories (the 10 first)<br>
  Dim.1<br>
ROE_1  0.066<br>
ROE_2  1.619<br>
ROE_3  0.723<br>
ROE_4  0.359<br>
ROE_5  -0.807<br>
ROE_6  -0.145<br>
ROE_7  -0.586<br> 
ROE_8  -0.813<br>
ROE_9   0.307<br>
</em>

If the encoded variable ROE9 would be monotic versus STATUS (BADGOOD) then the coordinates of ROE_1 to ROE_9 on the first axis should be respect-full of the order 1 to 9 (Guttman effect)<br>
We will use this property in oreder to build a test for monotonicity which will be called "MCA Monotonicity test"

#### Performaing the MCA monotonicity test  all the ratio variables

The test is performed on the variables recommended for their monotonicity on page 160.<br>
to the exception of V95A-96, V110A-107 for the bin.var() function does not behave appropriatley  with parameters "bin.cut" and "proportions" 

- <strong>EBITDAON-87</strong> -> EBITDAonSALES	= Ratio EBITDA/Sales [%]
- <strong>ROI-88</strong> -> ROI	= Ratio EBIT/Operating Assets [%]
- <strong>ASSETSTU-92</strong> -> ASSETS_TURNOVER	= Ratio Total Assets/Turnover
- <strong>PAYABLES-97</strong> -> PAYABLES_PERIOD	= Ratio Trade Payables/Daily Purchases
- <strong>IEONLIAB-101</strong> -> IEonLIABLITIES	= Ratio Interest Expenses/Liabilities [%]
- <strong>IEONFINA-102</strong> -> IEonFINANCIAL_DEBTS	= Ratio Interest Expenses/Financial Debts [%]
- <strong>TRADEPA-109</strong> -> TRADE_PAYABLESonTL	= Ratio Trade Payables/Total Liabilities [%]
- <strong>EQUITYON-108</strong> -> EQUITYonPERMANENT_CAPITAL	= Ratio Equity/Permanent Capital [%]
- <strong>ROAMINUS-115</strong> -> ROAminusIEonTL	= ROA minus Ratio Interest Expenses/Total Liabilities


