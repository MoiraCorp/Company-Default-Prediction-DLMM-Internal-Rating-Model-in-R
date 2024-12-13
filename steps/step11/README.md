Here we follow step by step the contents of Chap. 4, section 4.5.10 :  Summary table of indicators and short listing, pp. 177-184<p>

In order to fill the synoptic table some of the operations performed in the previous sections need to be applied to the 34 Ratios Variables: ROE at wcs2train[86] to ROETR at wcs2train[119].

> ratiovars <- c(86:119)<br>
> wcs2train.ratios <- wcs2train[ratiovars]<br>
> sapply(wcs2train.ratios, class)
