# One by one empirical analysis of variables 

It follows the section: 4.5.2 Empirical assessment of working hypothesis (page 133 of the DLMM book)<br>
We want to compute the "descriptive statistics" for each good/bad group for each of the following variables :
<ul>
<li><strong>ROE</strong> (Ratio Net Profit/Equity)</li>
<li><strong>IEONLIAB</strong>  (Ratio Interest Expenses/Liabilities [%])</li>
<li><strong>V110A</strong>  (Ratio Inventories/Total Assets [%])</li>
</ul>

We use the package "psych" in R (it is usually avalaible in the standard installation of R?) https://cran.r-project.org/web/packages/psych/psych.pdf <br>
In this package we use function describeBy() in order to provides variable basic statistics for each of the "bad" and "good" classes<br>
Each variable basic statistics table is saved in a separate .csv file

### Loading the "psych" package
> library(psych)

### Computing basic good-bad satistics for variable: ROE (Ratio Net Profit/Equity)
> mt_dat <- describeBy(wcs2train$ROE, wcs2train$BADGOOD, mat=T)<br>
> write.csv(mt_dat, file = "C:/Projets_En_Cours/AI_MTPL/UCI_Internal_Ratings/R Notes/describe_ROE.csv")<br>
> mt_dat<br>

<em>The last command generates the following output:</em><br>
    item group1 vars    n      mean        sd median  trimmed      mad   min   max range     skew  kurtosis       se<br>
X11    1  "Bad"    1   51 418.88892 2537.3339  0.487  6.87900 24.78907  -525 17930 18455 6.456552  41.49815 355.2978<br>
X12    2 "Good"    1 1221  45.73707  459.6099 10.000 17.53419 31.45188 -5500  8300 13800 5.809446 139.28237  13.1532<br>

### Computing basic good-bad satistics for variable: IEONLIAB (Ratio Interest Expenses/Liabilities [%])
> mt_dat <- describeBy(wcs2train$IEONLIAB, wcs2train$BADGOOD, mat=T)<br>
> write.csv(mt_dat, file = "C:/Projets_En_Cours/AI_MTPL/UCI_Internal_Ratings/R Notes/describe_IEONLIAB.csv")<br>
> mt_dat<br>

<em>The last command generates the following output:</em><br>
    item group1 vars    n      mean        sd median  trimmed      mad   min   max range     skew  kurtosis       se<br>
X11    1  "Bad"    1   51 6.487020 14.562831  4.524 4.421317 2.244656   0 107.407 107.407 6.516170 42.225823 2.03920416<br>
X12    2 "Good"    1 1221 3.820161  2.567423  3.480 3.604277 2.379573   0  23.950  23.950 1.293554  4.471053 0.07347501

### Computing basic good-bad satistics for variable: V110A (Ratio Inventories/Total Assets [%])
> mt_dat <- describeBy(wcs2train$V110A, wcs2train$BADGOOD, mat=T)
> write.csv(mt_dat, file = "C:/Projets_En_Cours/AI_MTPL/UCI_Internal_Ratings/R Notes/describe_V110A.csv")<br>
> mt_dat<br>

<em>The last command generates the following output:</em><br>
    item group1 vars    n      mean        sd median  trimmed      mad   min   max range     skew  kurtosis       se<br>
X11    1  "Bad"    1   51 26.91231 23.82903 22.537 23.82188 20.9521   0  95.888  95.888 1.034288 0.5017606 3.3367317<br>
X12    2 "Good"    1 1221 20.85190 23.25327 12.832 16.66432 17.5955   0 101.529 101.529 1.421104 1.4549385 0.6654664<br>

### Compare with corresponding results presented in DLMM Book

<img src="./assets/Table_4_6_Page 133_Describe_3Ratio.JPG" alt="drawing" width="100%"/>
<em>NOTE</em> : The "pretty" presentation of the variable statistics was created by collating the 3 .csv tables in one .xls table
using Edit-Paste Special-Tanspose in OpenOfficeCalc<br>
Also, correct printing to pdf in "Lanscape" mode was set using the File-Page Preview option<br>

<br><strong>The descriptive statistics match those presented in page 133 of the DLMM book.</strong><br>
<em>NOTE</em> : The last term ("se") listed by the describeBy() function is what is called the Standard Error of the mean as explained in page 132 of the DLMM book.
