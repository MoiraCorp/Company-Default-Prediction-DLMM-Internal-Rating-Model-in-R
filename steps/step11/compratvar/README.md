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

The 3 difference vectors <a id="raw-url" href="https://github.com/MoiraCorp/DLMM-IRating-in-R/blob/main/steps/step11/compratvar/assets/INDC3.csv">INDC3.csv</a><br>
are added as columns to the synoptic table: <a id="raw-url" href="https://github.com/MoiraCorp/DLMM-IRating-in-R/blob/main/steps/step11/relpro/assets/Ratios_Synoptic_De%20Laurentis.xls">Ratios_Synoptic_De Laurentis.xls</a><br>
These 3 columns are named: "Align. Mean", "Align. Trimmed", "Align. Median". <br>
The sign of the each of the differences (ex: mean(“Good”)-mean(“Bad”) is then compared with the sign of the column “Theory sign f(p(D))” (see Section 10a)<br>
In each of the 3 columns, a “Y” is placed if the sign of the variation is in agreement with the model proposed by the author. Otherwise, it is a “N”.

Illustrated in: Ratios_Synoptic_De Laurentis.jpg
<img src="./assets/Ratios_Synoptic_De Laurentis.jpg" alt="drawing" width="100%"/>

**We note a VERY GOOD COHERENCE with the model proposed by the author in term of the sign of the relation between Ratio Variables and the population of “Default” companies**
