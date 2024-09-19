# One by one empirical analysis of variables 

It follows the Chapter 4 section in 4.5.2 Empirical assessment of working hypothesis (page 133)<br>
We want to compute the "descriptive statistics" for each good/bad group for each of the following variables :
<ul>
<li><strong>ROE</strong> (Ratio Net Profit/Equity)</li>
<li><strong>IEONLIAB</strong>  (Ratio Interest Expenses/Liabilities [%])</li>
<li><strong>V110A</strong>  (Ratio Inventories/Total Assets [%])</li>
</ul>

We use the package "psych" in R (it is usually avalaible in the standard installation of R?) https://cran.r-project.org/web/packages/psych/psych.pdf <br>
In this package we use function describeBy() in order to provides variable basic statistics for each of the "bad" and "good" classes<br>
