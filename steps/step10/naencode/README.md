## Replacement of NA encoded outliers by interpolation

In the previous section (step9), we have detected “extreme outliers” and encoded them as NA (not Available)<br>
However, most AI methods require the processing FULL datatables.<br>

The authors propose to “fill in” the masqued outliers with either the mean or the median of each of the Ratio Variable statistical distribution.<br>
Although it is common practice, <em>this method is based on a very thin probability theory argument</em>.<br>
The present dataset being essentially “multidimensional” it is better justified to proceed with the replacement of the NA values on the basis of the multidimensional relations existing between the Ratio Variables rather than processing them individually.

### Comparison of Ratio Variables range and statistics before and after “outliers” processing

### Study of Ratio Variables correlation properties after “outliers” processing
