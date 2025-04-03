#  Experimenting with Stepwise Linear Discriminant Analysis

## Purpose

When LDA uses a large number of predicting variables (here, ratios) of predictors, the stepwise method can be useful by automatically selecting the "best" variables to use in the model. The stepwise method starts with the variable which separates the groups the most and follows by adding new variables in such a way that a global level of separability criteria is maintained. The inclusion of new variables is stopped if the level of separability criteria is degraded under limit value set by the user.

The Wilk's Lambda criterion is usually the adopted separability criterion. (see -> https://en.wikipedia.org/wiki/Wilks%27s_lambda_distribution)<br>


## Method

> <p><strong>Stepwise LDA on original data</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step13/stepwise)</p>
> <p><strong>Applying authors recommended stepwise LDA</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step13/authstepw)</p>

