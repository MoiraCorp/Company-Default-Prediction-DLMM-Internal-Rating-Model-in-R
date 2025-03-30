## Exploring Gaussian Copula encoding (Anamorphosis) 

The gaussian anamorphosis, known also as **Gaussian Copula encoding** is a mathematical function which transforms a variable X with any density distribution into a new variable Y with a Gaussian density distribution. As the Linear Discriminant Analysis method is based on the comparison between GOOD and BAD groups which variables are normaly distributed (idem, Guassian), Gaussian Copula encoding is a way to adapt the data so that it optimaly fits the LDA instrument. 

This aspect of data pre-processing is addressed by the authors in section 4.5.9 Transformationof indicators (pages: 164-177). Although it is there essentially based on the use of formula based transformations and not in terms of a transformative transition between probability distributions.
We have in particular evaluated the use of the LOGIT recoding function in: evaluated Step10 - Transformation of indicators using a logistic formula: the case of the ROE ratio - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step10/logencode)

Mahalanobis distance
<img src="./assets/mahalanobis distance.jpg" alt="drawing" width="100%"/>

Illlustration of LDA with two groups
<img src="./assets/GUID-B739E00B-9BDB-4BDE-963A-B2B17D5FB222-web.png" alt="drawing" width="100%"/>

Greenacre, Michael, and Paul Lewi. "Distributional equivalence and subcompositional coherence in the analysis of compositional data, contingency tables and ratio-scale measurements." Journal of Classification 26.1 (2009): 29-54.
