## Developing a var/BADGOOD monotonicity detection scheme

#### Testing MCA for detecting monotonicity

Building a data.frame ROE9vSTATUS containing the cross-table between the binned ROE9 variable (ROE binned in 9 levels) versus STATUS variable <br>
It needs to use the bin.var() function which R code has neen introduced in this exrecise in the section: step7-binning<br>
and the R FactoMineR package -> https://cran.r-project.org/web/packages/FactoMineR/index.html<br>

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

#### Building an equipopulated encoding for all the ratio variables
