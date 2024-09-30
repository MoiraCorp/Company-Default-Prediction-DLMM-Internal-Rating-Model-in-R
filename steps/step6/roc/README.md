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
> ##### <em>The printed output is:
[1] 0.0429671</em><br>

The results obtained for the 3 variables: ROE,IEONLIAB and V110A, namely R tables: roc1,roc2 and roc3<br>
> roc1 = roc(wcs2train$BADGOOD, wcs2train$ROE)<br>
> roc2 = roc(wcs2train$BADGOOD, wcs2train$IEONLIAB)<br>
> roc3 = roc(wcs2train$BADGOOD, wcs2train$V110A)<br>

followed by:
> roc1_result <- c(auc1[1], vr1, ci1[1], ci1[3])<br>
> roc2_result <- c(auc2[1], vr2, ci2[1], ci2[3])<br>
> roc3_result <- c(auc3[1], vr3, ci3[1], ci3[3])<br>

are collated in table ROCS3.csv and presented in Fig_4_15_Page 155-156_ROC Tests.pdf
<img src="./assets/Fig_4_15_Page 155-156_ROC Tests.JPG" alt="drawing" width="80%"/>

### ROC curves graphical representation
Here we use the ggroc() function from the pROC package -> https://cran.r-project.org/web/packages/pROC/index.html<br>
> ggroc(list(ROE=roc1, IEONLAB=roc2, V110A=roc3), size=1) + ggtitle("ROC for 3 typical ratios versus BADGOOD assignment") + theme(plot.title = element_text(hjust = 0.5))<br>

The resulting curves are presented in Fig_4_15_Page 155-156_ROC Curves.pdf
<img src="./assets/Fig_4_15_Page 155-156_ROC Curves.JPG" alt="drawing" width="60%"/>

### Computing ROC test on the whole set of variables
We are build a similar ROS results table (ex; ROOCS3) for all the whole set of ratio variables from ROE to ROETR<br>
The position of these starting and ending ratios inside the wcs2train dataframe are respectively :<br>
ROE at wcs2train[86] and ROETR at wcs2train[119]<br>

We are scanning all the columns of wcs2train table from index 86 to index 119
and compute their RCS test results which are placed in table ROCSF which is saved in the file ROCSF.csv

> varcount = 0<br>
> for(i in 86:119){<br>
	rocr = roc(wcs2train$BADGOOD, wcs2train[,i])<br>
	aucr <- auc(rocr)<br>
	cir <- ci(rocr)<br>
	vrr <- var(rocr)^0.5<br>
	rocr_result <- c(aucr[1], vrr, cir[1], cir[3])<br>
	varcount = varcount + 1<br>
	if (varcount == 1){<br>
		ROCSR <- data.frame(rocr_result)<br>
		names(ROCSR)[varcount] <- colnames(wcs2train)[i]<br>
	} else {<br>
		ROCSR <- cbind(ROCSR, data.frame(rocr_result))<br>
		names(ROCSR)[varcount] <- colnames(wcs2train)[i]<br>
	}<br>
}<br>
> rownames(ROCSR) <- c("Area", "Std. Error", "Lower Bound", "Upper Bound")
> #### Transposing the table
> ROCSF <- t(ROCSR)<br>
> write.csv(ROCSF, file = "C:/Projets_En_Cours/AI_MTPL/UCI_Internal_Ratings/R Notes/ROCSF.csv")<br>

The table of ROC test results for all ratios is presented in  : ROC_All ratios_v_BADGOOD_Page 157.pdf
<img src="./assets/ROC_All ratios_v_BADGOOD_Page 157.JPG" alt="drawing" width="100%"/>

Following the recommandations of the author, the ratios with best separation (AuROC >= 0.62) are:<br>

- DEBTEQUTR	Interest-bearing Financial Debt/Equity	
- EBITDAIE	EBITDA/Interest Expenses
- ASSETSTU	Sales/Total Assets
- V95A		Inventory/Daily Sales
- IEONEBIT	Interest Expenses/EBITDA [%]
- COMMERCI	(Trade Receivables + Inventory – Trade Payables)/Daily Sales
- TRADEPA.	Trade Payables/Total Liabilities [%]
- ROAMINUS	ROA –  Interest Expenses/Total Liabilities<br>

<em>NOTE  :</em> None of the 3 variables studied so far  : ROE, IEONLIAB and V110A are is this «  best  » pack  !<br>
Also, DEBTEQUTR is a combined variable added “on purpose (ad-hoc ?) by the author at the end of the table

### Contrasting the ROC curves for the best and the worst seoaration index
We are also presenting on the same graph, the ROC curves for  :
- the best BAD-GOOD separator ratio, DEBTEQUTR with an AuROC = 0.667
- the worst BAD-GOOD separator ratio, EXTRIC with an AuROC = 0.465, which is below the 50%-50% separation (AuROC = 0.5)<br>

> roc1 = roc(wcs2train$BADGOOD, wcs2train$DEBTEQUTR)<br>
> roc2 = roc(wcs2train$BADGOOD, wcs2train$EXTRIC)<br>
> ggroc(list(DEBTEQUTR=roc1, EXTRIC=roc2), size=1) + ggtitle("ROC for best-worse ratios versus BADGOOD assignment") + theme(plot.title = element_text(hjust = 0.5)) +  geom_abline(intercept=1, slope=1)<br>

<em>NOTE :</em> The geom_abline() function from th ggplot2 package traces the 0.5 AuROC curve which represents the H0 (zero) hypothetis or 50%-50% separation

The illustration is saved in: ROC_Best-Worst ratios_v_BADGOOD_Page 157.pdf



