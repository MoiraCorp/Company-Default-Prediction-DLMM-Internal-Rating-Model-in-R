Here we follow step by step the contents of Chap. 4, section 4.5.10 :  Summary table of indicators and short listing, pp. 177-184<p>

## Purpose

## Method

In order to fill the synoptic table some of the operations performed in the previous sections need to be applied to the 34 Ratios Variables: ROE at wcs2train[86] to ROETR at wcs2train[119].

> ratiovars <- c(86:119)<br>
> wcs2train.ratios <- wcs2train[ratiovars]<br>
> sapply(wcs2train.ratios, class)

##### <em>The printed output is:
  ROE  EBITDAON       ROI       ROA      V89A       ROS  ASSETSTU  INVENTOR  RECEIVAB      V94A      V95A  PAYABLES  COMMERCI<br>
  IEONEBIT  NIEONEBI  IEONLIAB IEONFINA.    EXTRIC  TAXESONG<br> 
  "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric"<br>
  "numeric" "numeric" "numeric" "numeric" "numeric" "numeric"<br> 
  INTANGIB  TRADERE.     V110A  EQUITYON  TRADEPA.   DEBTEQU   CURRENT   QUICKRA  SALESONV  SALESMIN  ROAMINUS  EBITDAIE<br>
  EQUILIABL   DEBTEQUTR     ROETR<br> 
  "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric" "numeric"<br>
  "numeric"   "numeric" "integer"
</em>


> <p><strong>Theoretical relation as a function of probability of default f(p(D)) </strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step11/relpro)</p>
> <p><strong>Empirical Monotonicity determination</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step11/empmono)</p>
> <p><strong>Comparative BAD/GOOD for Ratio Variables statistical distributions</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step11/compratvar)</p>
> <p><strong>Histograms and Normality hypothesis for Ratio Variables</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step11/normratvar)</p>
> <p><strong>Measures of separability between GOOD and BAD (idem, Default) groups</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step11/sepratvar)</p>
> <p><strong>Correlation between Ratio Variables</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step11/corrratvar)</p>
