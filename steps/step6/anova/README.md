### ANOVA of variable-BADGOOD assocation

> wcs2train.lmROE = lm(ROE ~ BADGOOD, data = wcs2train)<br>
> summary(wcs2train.lmROE)<br>
> anvROE <- anova(wcs2train.lmROE)<br>
> write.csv(anvROE, file = "C:/Projets_En_Cours/AI_MTPL/UCI_Internal_Ratings/R Notes/anvROE.csv")<br>

This code is repeated for variables IEONLAB and V110A saving the results in tables: anvIEONLIAB.csv and anvV110A.csv<br>

The results for the 3 variables ROE, IEONLAB and V110A are collated in one table in Table_4_13_ANOVA.xls<br> 
in order to match the presentation in the DLMM book on page 150<br>

#### ETA – Measure of variable-BADGOOD association
Eta-squared is the sample proportion of variance explained in a numerical variable by a categorical predictor variable. 
Eta2 is computed as between-groups sum of squares divided by total sum of squares. Eta is the square root of Eta.

It is computed from inside the file Table_4_13_ANOVA.xls
<img src="./assets/anova/Table_4_13_ANOVA.JPG" alt="drawing" width="100%"/>
