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

### Testing the discrimatory power of regrouped sectors
