## Comparative BAD/GOOD for Ratio Variables statistical distributions

As in Section 2, we are using the describeBy() function from R package psych in order to extract for each Ratio Variable:
the mean, the “trimmed” mean and the median.
For robustness of the results, we are using datatable wcs2train.ratios.MON. In this table, “extreme” outliers
and odd values for INVENTOR, V95A and V110A have been encoded as NA. They are not part of the calculation.

The differerences between the values: mean, “trimmed” mean and median for each of the “Good” and “Bad” (idem, Default)
are computed and saved in the INDC3 datatable.

> library(psych)
> j = 0
> for(i in 1:34){ <br>
	j = j + 1 <br>
	mt_dat <- describeBy(wcs2train.ratios.MON[,i], wcs2train$BADGOOD, mat=T) <br>
	if(i == 1){ <br>
		INDC3 <- data.frame(c(mt_dat$mean[1]-mt_dat$mean[2], mt_dat$trimmed[1]-mt_dat$trimmed[2], mt_dat$median[1]-mt_dat$median[2])) <br>
		names(INDC3)[j] = names(wcs2train.ratios.MON)[i] <br>
	} else  { <br>
		indcx <- data.frame(c(mt_dat$mean[1]-mt_dat$mean[2], mt_dat$trimmed[1]-mt_dat$trimmed[2], mt_dat$median[1]-mt_dat$median[2])) <br>
		INDC3 <- cbind(INDC3, indcx) <br>
		names(INDC3)[j] = names(wcs2train.ratios.MON)[i] <br>
	} <br>
} <br>
> write.csv(INDC3, file = "C:/Projets_En_Cours/AI_MTPL/UCI_Internal_Ratings/R Notes/INDC3.csv")


