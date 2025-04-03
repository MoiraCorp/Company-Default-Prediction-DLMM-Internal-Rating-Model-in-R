#  Experimenting with Stepwise Linear Discriminant Analysis

## Purpose

When LDA uses a large number of predicting variables (here, ratios), the stepwise method can be useful by automatically selecting the "best" variables to use in the model. The stepwise method starts with the variable which separates the groups the most and follows by adding new variables in such a way that a global level of separability criteria is maintained. 

The Wilk's Lambda criterion is usually the adopted separability criterion. (see -> https://en.wikipedia.org/wiki/Wilks%27s_lambda_distribution)<br>

The Wilk's Lambda criterion scale of ranges from 0 to 1, where 0 means total discrimination, and 1 means no discrimination. Each new independent variable is tested by putting it into the model and then taking it out, thus generating a Λ (Lambda) statistics which is a measure of association between the new variable and the group of those already present in the model.<br>
The significance of the change in Λ between the new variables to be added to the xisting group of variables is measured with an F-test (idem, ANOVA Fisher Test on the equality of means). If the F-value is greater than the critical value (by default, 3.84), the variable is added in the model.<br>

**IMPORTANT NOTES:**
  -  The ANOVA Fisher test implies that the **predicting variables are Normally distributed** (idem, display a Gaussain probability density)
  -  The Stepwise produres implies that the predicting variables are independent variables. This necessitates a preprocessing phase which is usually conducted in LDA by the determination of the best discriminant feature space. The **axes of this feature space are usually the predicting variables used by the Stepwise LDA method** (ex: LD1,LD2 in the illustation presented at -> https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step12).


## Method

> <p><strong>Stepwise LDA on original data</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step13/stepwise)</p>
> <p><strong>Applying authors recommended stepwise LDA</strong> - -> (https://github.com/MoiraCorp/DLMM-IRating-in-R/tree/main/steps/step13/authstepw)</p>

