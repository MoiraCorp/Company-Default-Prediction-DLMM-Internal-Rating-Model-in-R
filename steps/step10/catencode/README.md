## Re-binning categorical variables: the case of the SECTOR variable

### Regrouping sparse company sector categories

In the datatable used in the book, there is only one category variable (idem., qualitative), which is SECTOR, the encoding of the sector of activity.
Unfortunately, for some companies’ sector, the table is fairly sparse. In order to manipulate a better “balanced” distribution, SECTOR categories need to be regrouped.<p>

For aggregating sectors, the best could be probably to generate a form of similarity abalysis based on the Ratios Variables corrected from extreme outliers.
For this purpose we are evaluating the Analysis of Similarities ANOSIM method (https://www.rdocumentation.org/packages/vegan/versions/2.3-5/topics/anosim)<br>

> install.packages("vegan")<br>
> library(vegan)<br>
> sector.ano <- anosim(wcs2train_CT,wcs2train$SECTOR)<br>
> plot(sector.ano)<br>

<em>NOTE:</em> Due to computation time, it is probably more efficient to work with a limited number of principal components extracted from a prior PCA of the Ratio Variables datatable<p>

The results are illustrated in: Table_4_22b_page 172_SECTOR Group similiraties.pdf<br><br>
<img src="./assets/Table_4_22b_page 172_SECTOR Group similiraties.JPG" alt="drawing" width="80%"/>

From the illustration, one can suggest the following regrouping:<br>
	SC1:	482<br>
	SC2:	430<br>
	SC3:	614, 490, 480<br>
	SC4:	492, 481, 600, 615, (450)<br>
	SC5:	All others<br>
 <em>These results are similar to those proposed empirically by the authors on page 172</em>

### Testing the discrimatory power of regrouped sectors

> table(wcs2train$SECTOR, wcs2train$BADGOOD)<br>
> sector_recoded <- subset(wcs2train, select=c("SECTOR"))<br>
> sector_recoded$SECTOR3 <- revalue(sector_recoded$SECTOR, c(<br>
	'"482"'='SC1',<br>
	'"430"'='SC2',<br>
	'"614"'='SC3','"490"'='SC3','"480"'='SC3',
	'"492"'='SC4','"481"'='SC4','"600"'='SC4','"615"'='SC4','"450"'='SC4',<br>
	'"258"'='SC5','"268"'='SC5','"273"'='SC5','"280"'='SC5','"294"'='SC5','"431"'='SC5','"470"'='SC5','"473"'='SC5','"491"'='SC5','"NA"'='SC5'))<br>
> table(sector_recoded$SECTOR3, wcs2train$BADGOOD)

##### <em>The printed output is:
| Group code | "Bad" | "Good" |
| ---------- | ----- | ------ |
| SC5 | 0 | 12 |
| SC2 | 33 | 712 |
| SC4 | 5 | 160 |
| SC3 | 6 | 101 |
| SC1 | 7 | 236 |
</em>

> tbl <- table(sector_recoded$SECTOR3, wcs2train$BADGOOD)<br>
> chisq.test(tbl)

##### <em>The printed output is:
data:  tbl<br>
X-squared = 2.7683, df = 4, p-value = 0.5973<br>
</em>

