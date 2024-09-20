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

#### Each of these table() objects need to be converted into dataframes for later concatenation
> cTabdf <- as.data.frame.matrix(cTab)<br>
> cTabidf <- as.data.frame.matrix(cTabi)<br>
> cTabjdf <- as.data.frame.matrix(cTabj)<br>

#### Adding a "total sum" column to each of these marginal tables
> cTabdf$total <- cTabdf[,1] + cTabdf[,2]<br>
> cTabidf$total <- cTabidf[,1] + cTabidf[,2]<br>
> cTabjdf$total <- cTabjdf[,1] + cTabjdf[,2]<br>

#### Multiplying by 100.0 the last 2 tables in order to conform to the DLMM book text and reduce the numeric format to one decimal after decimal point
> indx <- sapply(cTabidf, is.numeric)<br>
> cTabidf[indx] <- lapply(cTabidf[indx], function(x) x*100.0)<br>
> cTabidf[indx] <- lapply(cTabidf[indx], function(x) format(round(x, 1), nsmall = 1))<br>
> indx <- sapply(cTabjdf, is.numeric)<br>
> cTabjdf[indx] <- lapply(cTabjdf[indx], function(x) x*100.0)<br>
> cTabjdf[indx] <- lapply(cTabjdf[indx], function(x) format(round(x, 1), nsmall = 1))<br>

#### Row names(here: Sector Code) need to be added as a new column to these dataframes before concatenation
> names <- rownames(cTabdf)<br>
> cTabr <- cbind(names, cTabdf)<br>
> cTabir <- cbind(names, cTabidf)<br>
> cTabwi <- merge(cTabr, cTabir, by="names")<br>
> cTabjr <- cbind(names, cTabjdf)<br>
> cTabwij <- merge(cTabwi, cTabjr, by="names")<br>

#### The resulting table is exported to a .csv file
> write.csv(cTabwij, file = "C:/Projets_En_Cours/AI_MTPL/UCI_Internal_Ratings/R Notes/defaultrates_sector.csv")

### Display and interpretation
<img src="Table_4_8_Page 138_Default_Sectors.JPG" alt="drawing" width="70%"/>

