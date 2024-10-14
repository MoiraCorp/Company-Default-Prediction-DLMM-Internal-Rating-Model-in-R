# Analysis of outliers

This implementation follows step by step the content of Chap. 4, section 4.5.8 :  analysis of outliers, pp. 162-164<br>

## Purpose

## Method

The authors base their approach on the use of the “interquartile range” (IQR).<br>
More precisely they name “outliers”, those samples which values are higher than the 3rd quartile (Q3) and lower than the 1st quartile (Q1).

> <p><strong>Computing the number of outliers for the ration ROE (page 163) </strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step9/roeoutlr)</p>
> <p><strong>Computing outliers percentage for all the ratios</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step9/alloutlr)</p>
> <p><strong>Masking outlier's values using the NA R notation</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step9/naoutlr)</p>
