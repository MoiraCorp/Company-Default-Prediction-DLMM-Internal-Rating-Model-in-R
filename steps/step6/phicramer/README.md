## Phi and Cramer’s V measures
This implementation follows step by step the content of Chap. 4, section 4.5.5 :  Discriminant power, pp. 152<br>

Here we use the Phi() and CramerV() functions from the R DescTools package -> https://cran.r-project.org/web/packages/DescTools/index.html<br>

> install.packages("DescTools")<br>
> library(DescTools)<br>
> tbl <- table(wcs2train$SECTOR, wcs2train$BADGOOD)<br>

### Phi measure of association
> Phi(tbl)<br>
> ##### <em>The printed output is:
[1] 0.05802905
### Cramer measure of assoction
> CramerV(tbl)
> > Phi(tbl)<br>
> ##### <em>The printed output is:
[1] 0.05802905<br>

The 2 results are collated in Table_4_16_Page 152_Phi_CramerV.xls and presented in Table_4_16_Page 152_Phi_CramerV.pdf
