## ROC curves and Area under ROC (AuROC)

A ROC crurve (Receiver Operating Characteristic) tells how the sensitivity and specificity will trade off, 
if one uses different thresholds to convert the predicted probability into a predicted classification.<br> 
Since the predicted probability will be a function of the test result variable, it is also telling how they trade off 
if one use different test result values as a threshold.

This implementation follows step by step the content of Chap. 4, section 4.5.5 :  Discriminant power, pp. 152<br>

### ROC numerical summaries
Here we use the auc(), ci() and var() functions from the pROC package -> https://cran.r-project.org/web/packages/pROC/index.html<br>
> install.packages("pROC")<br>
> library(pROC)<br>
> roc1 = roc(wcs2train$BADGOOD, wcs2train$ROE)<br>

#### Printing the AuROC (Area under ROC curve)
> auc1 <- auc(roc1)
> ##### <em>The printed output is:
Area under the curve: 0.5927</em>

#### Printing the ROC asymptotic intervals
> ci1 <- ci(roc1)
> ##### <em>The printed output is:
95% CI: 0.5085-0.6769 (DeLong)</em>

#### Getting the Std. Error under a non parametric assumption
> vr1 <- var(roc1)^0.5
> > ##### <em>The printed output is:
[1] 0.0429671</em><br>

The results obtained for the 3 variables: ROE,IEONLIAB and V110A, namely R tales: roc1,roc2 and roc3<br>
are collated in table ROCS3.csv and presented in Fig_4_15_Page 155-156_ROC Tests.pdf

### ROC curves graphical representation
### Computing ROC test on the whole set of variables
