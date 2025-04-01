# Linear Discriminant Analysis - Initial approach

Here we follow step by step the contents of Chap. 4, section 4.6.2 : Linear discriminant analysis, pp. 185-210<br>

## Purpose

The authors are proposing to use Linear Discriminant Analysis method (LDA) in order to solve the problem of estimating the Probability of Default (PD) of a paticular company using its financial accounts.<br>
Like most of the Machine learning (ML) methods it is conducted in two phases:<br>
- A **training phase** which determines the statistical characteristics of a representative sample of both GOOD (idem, stable) companies and BD (idem, having defaulted companies). The parameters of the ML model are then determined from these from these characteristics.
- An **application (or prediction phase)** when the model is used in order to predict the Probability of Default (PD) of any other company over a period which is generally the next year

In the case of Linear Discriminant Analysis method (LDA):
- The **training phase** is conducted in two phases:
  1. Each group is characterized by its average vector (or center of gravity) **M** and its matrix of variane-covariance **Σ**
  2. The LDA algorithm determines a new set of coordinates which maximises the separability between groups. <br> (In the illustration below, we go from original dimensions to new LD1,LD2 dimensions))
- The **prediction phase** is also conducted in two phases
  1. The Mahanobis distance between a new company X and the center of a particular group is determined as : **D = (X - M)<sup>t</sup> * Σ<sup>-1</sup> * (X - M)**. In our case, two distances are computed: Dg (GOOD) and Db (BAD)
  2. The new company is then assigned to the closest group. The Mahalanobis distance being the square root of the negative log likelihood. The probabilty (idem, likelihood) of a company to belong to this group is the computed as: **p = 1/<sub>2</sub> * e<sup>-D<sup>2</sup></sup>**


The principles of Linear Discriminant Analysis (LDA)
<img src="./assets/Machine-Learning-7.jpg" alt="drawing" width="40%"/>  

<em>NOTE:</em> In the present problem, **we have 34 ratios (dimensions) in our data space**.

## Method

> <p><strong>Data preparation</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step12/dataprep)</p>
> <p><strong>First run LDA on original data</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step12/firstorgdat)</p>
> <p><strong>LDA on decorrelated variables using a prior PCA</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step12/priorpca)</p>
> <p><strong>Stepwise LDA on original data</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step12/stepwise)</p>
> <p><strong>LDA on full author’s datatable</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step12/fullauthdat)</p>
