## Measures of separability between GOOD and BAD (idem, Default) groups

### Chi-square-test 

The (Pearson Chi-square test essentially tests wether qualitative (idem, categorical) classes are associates to particular
values of a variable. In other terms, if this variable separates well the given qualitative classes.
Here the test is performed on all Ratio Variables and test the GOOD-BAD classes separability.

For this separability to be significant (idem, separability) the p-value of the Chi-square test should be below 0.05
Even if this level is not reached, the p-value provides an estimate of the separability potential of a given variable.

> j = 0
for(i in 1:34){ <br>
	j = j + 1 <br>
	tbl <- table(wcs2train.ratios.MON[,i], wcs2train$BADGOOD) <br>
	chi <- chisq.test(tbl) <br>
	pvalue <- chi[3] <br>
	if(i == 1){ <br>
		INDC7 <- data.frame(c(pvalue)) <br>
		names(INDC7)[j] = names(wcs2train.ratios.MON)[i] <br>
	} else  { <br>
		indcx <- data.frame(c(pvalue)) <br>
		INDC7 <- cbind(INDC7, indcx) <br>
		names(INDC7)[j] = names(wcs2train.ratios.MON)[i] <br>
	} <br>
} <br>
> write.csv(INDC7, file = "C:/Projets_En_Cours/AI_MTPL/UCI_Internal_Ratings/R Notes/INDC7.csv")
