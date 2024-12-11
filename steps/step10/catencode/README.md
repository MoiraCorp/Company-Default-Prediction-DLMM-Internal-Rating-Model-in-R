## Re-binning categorical variables: the case of the SECTOR variable

### Regrouping sparse company sector categories

In the datatable used in the book, there is only one category variable (idem., qualitative), which is SECTOR, the encoding of the sector of activity.
Unfortunately, for some companies’ sector, the table is fairly sparse. In order to manipulate a better “balanced” distribution, SECTOR categories need to be regrouped.<p>

For aggregating sectors, the best could be probably to generate a form of similarity abalysis based on the Ratios Variables corrected from extreme outliers.
For this purpose we are evaluating the Analysis of Similarities ANOSIM method (https://www.rdocumentation.org/packages/vegan/versions/2.3-5/topics/anosim)

### Testing the discrimatory power of regrouped sectors
