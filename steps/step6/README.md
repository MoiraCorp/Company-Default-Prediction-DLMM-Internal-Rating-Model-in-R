# Evaluating the good/bad discriminant power of a variable

It follows the section: 4.5.5 Discriminant power (page 145 of the DLMM book)<br>

### ANOVA of variable-BADGOOD assocation

> wcs2train.lmROE = lm(ROE ~ BADGOOD, data = wcs2train)<br>
> summary(wcs2train.lmROE)<br>
> anvROE <- anova(wcs2train.lmROE)<br>
> write.csv(anvROE, file = "C:/Projets_En_Cours/AI_MTPL/UCI_Internal_Ratings/R Notes/anvROE.csv")<br>

The 3 results are for variables ROE, IEONLAB and V110A arecollated in one table in Table_4_13_ANOVA.xls<br> 
in order to match the presentation in the DLMM book on page 150


### ETA – Measure of variable-BADGOOD association

### Chi-square (Pearson) test of association between two categorical variables SECTOR-BADGOOD

### Phi and Cramer’s V measures

### ROC curves and Area under ROC (AuROC) 
#### ROC numerical summaries
#### ROC curves graphical representation
#### Computing ROC test on the whole set of variables

