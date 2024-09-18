# Step1 - Converting SPSS formatted data

## Reading data from the Wiley Web Site

The data from the book is available in SPSS .sav format and available fror download from the Wiley site
https://www.wiley.com//legacy/wileychi/delaurentis/

In this page, the left "Supplementary material" list element points to a page asking for the term located on Page 106 of the book as loading keyword
Two data sets are proposed: SAS and SPSS-PASW. We have used the second one:
https://www.wiley.com//legacy/wileychi/delaurentis/supp/SPSS-PASW.zip

The package "haven" has been loaded from the USA-CA berkeley CRAN Repository

The RPackage Haven enables to read the SPSS format
https://cran.r-project.org/web/packages/haven/index.html

## Reading the full dataset and saving it to .csv

> library(haven)<br>
> wcs1org <- read_sav("C:/Projets_En_Cours/AI_MTPL/UCI_Internal_Ratings/SPSS-PASW/W_CS_1_OriginalDataSet.sav")<br>
> write.csv(wcs1org, file = "C:/Projets_En_Cours/AI_MTPL/UCI_Internal_Ratings/SPSS-PASW/W_CS_1_OriginalDataSet.csv")

## Reading the "training" dataset and saving it to .csv (page 116)

## Reading the "cleaned" training data set and saving it to .csv (page 129)


