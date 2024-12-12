## Using empirical « binning » proposed by authors on SALES in order to explore concordances of SALES level with default rate

> bookquant[2] = 1000<br>
> bookquant[3] = 7500<br>
> bookquant

##### <em>The printed output is:
       0% 33.33333% 66.66667%      100% 
        0      1000      7500    464186
</em>

> \# Encoding SALES as a factor<br>
> bins_cut = 3<br>
> for(j in 1:bins_cut) {<br>
> 	if(j == 1){<br>
> 		collist <- c(sprintf("%s_1","SALES"))<br>
> 	} else {<br>
> 		collist <- append(collist, sprintf("%s_%s","SALES",j))<br>
> 	}<br>
> }<br>
> SALES3 <- with(wcs2train, cut(wcs2train$SALES, bookquant, include.lowest = TRUE, labels=collist))<br>
> tbl <- table(SALES3, wcs2train$BADGOOD)<br>
> tbl
