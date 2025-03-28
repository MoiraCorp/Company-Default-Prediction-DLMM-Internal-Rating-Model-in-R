## Detecting LogNormal distributions and applying a Fisher transformation

We are here assessing the LogNormal nature of some of the distributions by using the so called Fisher Transform:<br>
z = 1/2 ln((1-r)/(1-r)) = arctanh(r)<br>
This transform meant to turn the distribution of a correlation coefficient r into a Normal Distribution.<br>
It needs the variable to be transformed into interval (-1, +1) before it is applied.

From previous step output (see -> Characterizing the form of the Ratio Variables distributions) it has beenestablished that  LogNormal distributed Ratio Variables are : ASSETSTU, INVENTOR, V95A, IEONLIAB, IEONFINA­, INTANGIB, V110A, DEBTEQUTR<br>
Their indexes in the wcs2train.ratios.MON datatable are: 7,8,11,16,17,20,22,33
