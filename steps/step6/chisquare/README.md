## Chi-square (Pearson) test of association between two categorical variables SECTOR-BADGOOD
Here we are mirroring the SPSS Chi-Square Independence Test -> https://www.spss-tutorials.com/spss-chi-square-independence-test/<br>
in order to mimic the results illustrated in Table 4.15 - Chi-square test presented in the DLMM book on page 151<br>
In order to do so, we need to perform the following tasks :
- Pearson Chi-Square test
- Likelihodd Ratio test
- Linear-by-Linear Association <br>

 <em>NOTE:</em> in the IBM's support page for SPSS, it is stated in a technote on the Chi² test:<br>
'The Crosstabs procedure includes the Mantel-Haenszel test of trend among its chi-square test statistics. ... <br>
The MH test for trend will be printed in the "Chi-Square Tests" table and labelled "Linear-by-Linear Association".'<br>

### Pearson Chi-Square test
Here we use the chisq.test() function from the standard R installation
> tbl <- table(wcs2train$SECTOR, wcs2train$BADGOOD)<br>
> chisq.test(tbl)<br>
##### <em>The printed output is:
&nbsp; Pearson's Chi-squared test<br>
&nbsp; data:  tbl<br>
&nbsp; X-squared = 4.2799, df = 18, p-value = 0.9996</em><br>

### Likelihood Ratio test
Here we use the likelihood.test() function from the R Deducer package -> https://www.rdocumentation.org/packages/Deducer/versions/0.7-9/topics/likelihood.test
> install.packages("Deducer")<br>
> library(Deducer)<br>
> likelihood.test(tbl)<br>
##### <em>The printed output is:
&nbsp; Log likelihood ratio (G-test) test of independence without correction<br>
&nbsp; data:  tbl<br>
&nbsp; Log likelihood ratio statistic (G) = 5.5663, X-squared df = 18, p-value = 0.997</em><br>

### Linear-by-Linear Association
Here we use the mantel.test() function from the R lazyWeave package -> https://www.rdocumentation.org/packages/lazyWeave/versions/3.0.2/topics/mantel.test<br>
The mantel.test() function performs a Mantel-Haenszel test for linear trend in two way tables
> install.packages("lazyWeave")
> library(lazyWeave)
> mantel.test(wcs2train$SECTOR, wcs2train$BADGOOD)
##### <em>The printed output is:
&nbsp; Mantel Haenszel Chi-Square Test for Two Way Tables<br>
&nbsp; data:  <br>
&nbsp; M^2 = 0.1454, df = 1, p-value = 0.703</em><br>
<em>NOTE</em>: It is worth noting that the result is slightly different from that of the one presented on page 151 of the  DLMM book<br>

The 3 test results are collated in Table_4_15_Page 151_Chi_Square_Tests.xls and presented in Table_4_15_Page 151_Chi_Square_Tests.pdf
<img src="./assets/Table_4_15_Page 151_Chi_Square_Tests.JPG" alt="drawing" width="50%"/>
