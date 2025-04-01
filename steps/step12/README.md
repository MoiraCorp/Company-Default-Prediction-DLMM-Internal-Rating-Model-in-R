# Linear Discriminant Analysis - Initial approach

Here we follow step by step the contents of Chap. 4, section 4.6.2 : Linear discriminant analysis, pp. 185-210<br>

## Purpose

The authors are proposing to use Linear Discriminant Analysis method (LDA) in order to solve the problem of estimating the Probability of Default (PD) of a paticular company using its financial accounts.<b>
Like most of the Machine learning (ML) methods it is conducted in two phases:<br>
- A **training phase** which determines the statistical characteristics of a representative sample of both GOOD (idem, stable) companies and BD (idem, having defaulted companies). The parameters of the ML model are then determined from these from these characteristics.
- A **application (or prediction phase)** when the model is used in order to predict the Probability of Default (PD) of any other company over a period which is generally the next year




## Method

> <p><strong>Data preparation</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step12/dataprep)</p>
> <p><strong>First run LDA on original data</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step12/firstorgdat)</p>
> <p><strong>LDA on decorrelated variables using a prior PCA</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step12/priorpca)</p>
> <p><strong>Stepwise LDA on original data</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step12/stepwise)</p>
> <p><strong>LDA on full author’s datatable</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step12/fullauthdat)</p>
