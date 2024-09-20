# Cross-tabulation 01STATUS versus Industry Sector Code

It follows the section: 4.5.2 Empirical assessment of working hypothesis (page 144 of the DLMM book)<br>
We want to compute a cross-table between the 01STATUS variable and the Industry Sector Code<br>
in order to visualise the possible influence of the Sector of activity of a company upon its probabibilty of being in default<br><br>

We use the standard table() R function for performing the cross-tabulations
### Building the cross tabulation

Relating to Benzecri tensor notations, the table on page 138 is a side by side juxtaposition of:<br>
pij, pij/pi., pij/pj. or more simply: pij, pij/pi, pij/pj<br>
Where i (lines or rows) are SECTOR (Sector Code) and j (columns) are BADGOOD (bad/good or default/non default)<br>
In the preceding notations, pi. and pj. are the rows and columns marginal frequencies<br>

#### Starting by building the cross-table structure
> cTab <- table(wcs2train$SECTOR, wcs2train$BADGOOD)

#### Extracting the marginal distributions
> cTabi <- prop.table(cTab, 1)<br>
> cTabj <- prop.table(cTab)<br>

Relating to Benzécri notation, cTabi is pij/pi and cTabj is pij/pj
