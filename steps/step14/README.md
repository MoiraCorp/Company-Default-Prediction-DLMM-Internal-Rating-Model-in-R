#  Gaussian Copula encoding scheme

## Purpose


The gaussian anamorphosis, known also as **Gaussian Copula encoding** is a mathematical function which transforms a variable X with any density distribution into a new variable Y with a Gaussian density distribution. As the Linear Discriminant Analysis method is based on the comparison between GOOD and BAD groups which variables are normaly distributed (idem, Gauss shaped density), Gaussian Copula encoding is a way to adapt the data so that it optimaly fits the LDA instrument. 

This aspect of data pre-processing is addressed by the authors in section 4.5.9 Transformation of indicators (pages: 164-177). Although it is there essentially based on the use of formula based transformations and not in terms of a transformative transition between probability distributions.
We have in particular evaluated the use of the LOGIT recoding function in: evaluated Step10 - Transformation of indicators using a logistic formula: the case of the ROE ratio - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step10/logencode)

The concept of transition between two probability distributions was first formulated by J. P. Benzécri, in 1963 in his development of Correspondence Analysis as an inductive linguistics method of stistical text analysis. (see ->  Benzécri, J.P., 1969. Statistical analysis as a tool to make patterns emerge from data. In Methodologies of pattern recognition (pp. 35-74). Academic Press. https://helios2.mi.parisdescartes.fr/~lerb/publications/HONOLULU.pdf)<br>

Illlustration of probability transition
<img src="./assets/Benzecri_Transition proba_01.jpg" alt="drawing" width="50%"/>

These concepts later inspired G. Matheron who had created a linear method for the interpolation of two dimensional fields known as "Kriging". As any linear probability implies using the hypothesis of Normally distributed  radom variables, G. Matheron sought to improve the perfomance of "Kriging" by applying a prior transition from observed probability distributions to Gauus shaped ones. Realizing that in practice probability transition could only be algorithmically implemented on discrete probability distributions, G. Matheron developed in 1976 both a discrete based interpolation method known as "Disjunctive kriging" and a probability transition algorithm under the name of "Gaussian Anamorphosis" (see -> Matheron, G. and Kleingeld, W.J., 1987. The evolution of geostatistics. In APCOM (Vol. 87, pp. 9-12) https://www.saimm.co.za/Conferences/Apcom87Geostatistics/009-Matheron.pdf )

## Method

> <p><strong>Exploring Gaussian Copula encoding</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step14/gausscop)</p>
> <p><strong>Testing GOOD-BAD separability with Uniform and Gaussian Copula encoding</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step14/unigausscopul)</p>
> <p><strong>Using Gaussian Copula encoding for LDA</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step14/gausscoplda)</p>
