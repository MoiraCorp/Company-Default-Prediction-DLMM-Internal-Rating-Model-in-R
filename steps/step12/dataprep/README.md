## Data preparation

At this point, we have the following datasets to work with:

	- wcs2train the original datatable where column wcs2train$BADGOOD contains the GOOD-BAD (or default) company category
	- wcs2train.ratios is a datable extracted from wcs2train and restricted to the Ratio Variables of ranks 86 to 119 in the wcs2train table
	- wcs2train.ratios.NA is the wcs2train.ratios datatable where "extreme" outliers values have been turned into NAs
	- wcs2train.ratios.CT is the wcs2train.ratios.NA datable where NAs have been interpolated
	- wcs2train.ratios.MON is the wcs2train.ratios.NA datatable where overabundant 0s and 1s in INVENTOR, V95A and V110A have been turned into NAs

 Most of the processing functions that we will be using will require that one datatable be generated were the BADGOOD vector be appended to the datatable.
Ex: wcs2trainL <- cbind(wcs2train$BADGOOD, wcs2train.ratios)

In order to compare method results on an objective ground, one needs also to process the same datatable as the authors
From Page 188, the author signals that he is using the datatable: W_CS_1_AnalysisSampleDataSet_8MDA.sav

> library(haven)
> wcs2train8MDA <- read_sav("C:/Projets_En_Cours/AI_MTPL/UCI_Internal_Ratings/SPSS-PASW/W_CS_1_AnalysisSampleDataSet_8MDA.sav ")
> write.csv(wcs2train8MDA, file = "C:/Projets_En_Cours/AI_MTPL/UCI_Internal_Ratings/SPSS-PASW/ W_CS_1_AnalysisSampleDataSet_8MDA.csv")

After this operation, the file has been re-loaded after shortening the variable names following our conventions:

> wcs8trainMDA <- read.csv("C:/Projets_En_Cours/AI_MTPL/UCI_MTPL_Internal_Ratings/SPSS-PASW/W_CS_1_AnalysisSampleDataSet_8MDA.csv", header=TRUE, sep=",")

We then proceed to the extraction of the Ratio Variables and their “binned” transformations following the list proposed by the author on page 185,
namely: ROE to ROETR3A and T2ROE, OVERSECT430_614, SALESBin2cl1	SALESBin2cl2<br>
However, the xx3A variables are similar to our wcs2train.ratios.CT and they should not be left in the datatable because they are 95% redundant with the original Ratio Variables

This translates into the following list of indexes: 86:154, 156, 158, 161, 162 to which we add column 2 which contains the BADGOOD variable

> vars <- c(2, 86:154, 156, 158, 161, 162)
> wcs8train.vars <- wcs8trainMDA[vars]


**IMPORTANT NOTE**        : In our case, in the datatable, there is a large difference in population between GOOD Class = 1221 and the BAD class = 51 (Population total = 1272)
This would give for each class and “a priori” probalility of p(GOOD) = 0.96 and p(BAD) = 0.04 (a factor of 24 !)
The LDA method as well as the LOGIT method are based on the Bayes Decision rule which assigns companies on the basis of p(C)*p(C/whole population)
This type of formula should make use og p(GOOD) abd P(BAD) taken from the “observed” population

HOWEVER, in pratice, much better results are obtained in LDA when “a priori” probabilities have been made equal (idem, p(GOOD)=p(BAD)=0.5)

In the following steps we are going to **evaluate the improvements introduced by pre-processing the data** (wcs2train.ratios, wcs2train.ratios.CT, wcs2train.ratios.MON)
and will **compare the results with those obtained with the final encoding porposed by the author in the wcs8trainMDA datatable;.**



