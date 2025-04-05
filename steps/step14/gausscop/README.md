## Exploring Gaussian Copula encoding

In order to transform each ratio variable so that its final distribtion is Gaussian shaped, we are using a 2 steps procedure:
  - In the first step, the variable is encoded on 256 discrete intervals such as each of these intervals holds the smae amount of companies (idem, isopulation encoding)
  - In the second step, a transition table is aplied to these 256 intervals so that the final encoded variable display a Gauss shaped distribution

For the second step, the transition table (name tgauss) is borrowed from the Minimimage software which was developed at CTAMN-Ecole des Mines de Paris for the the purpose of satellite image processing and released as open code written in Delphi-Pascal (see -> https://code.google.com/archive/p/teravue-16bits-delphi/ )

> \# The Gauss conversion table used in Minimage coiso.pas subroutine<br>
> tgauss <- c(  0, 14, 24, 31, 36, 40, 43, 46, 48, 50, 52, 54, 56, 58, 59, 61,<br>
        62, 63, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78,<br>
        79, 79, 80, 81, 82, 82, 83, 84, 85, 85, 86, 87, 87, 88, 89, 89,<br>
        90, 90, 91, 92, 92, 93, 93, 94, 95, 95, 96, 96, 97, 97, 98, 98,<br>
        99, 99,100,100,101,101,102,102,103,103,104,104,105,105,106,106,<br>
       107,107,108,108,109,109,110,110,111,111,111,112,112,113,113,114,<br>
       114,115,115,115,116,116,117,117,118,118,118,119,119,120,120,121,<br>
       121,121,122,122,123,123,124,124,124,125,125,126,126,126,127,127,<br>
       128,128,129,129,129,130,130,131,131,131,132,132,133,133,134,134,<br>
       134,135,135,136,136,137,137,137,138,138,139,139,140,140,140,141,<br>
       141,142,142,143,143,144,144,144,145,145,146,146,147,147,148,148,<br>
       149,149,150,150,151,151,152,152,153,153,154,154,155,155,156,156,<br>
       157,157,158,158,159,159,160,160,161,162,162,163,163,164,165,165,<br>
       166,166,167,168,168,169,170,170,171,172,173,173,174,175,176,176,<br>
       177,178,179,180,181,182,183,184,185,186,187,188,189,190,192,193,<br>
       194,196,197,199,201,203,205,207,209,212,215,219,224,231,241,255)<br>

For illustration, we are applying this Gaussian Copula coding schme to the ROE ratio data form the wcs2train datatable.<br>
We are using two functions which are avilable in the standard R package:
 - the quantile function (-> https://www.rdocumentation.org/packages/stats/versions/3.6.2/topics/quantile )
 - the .bincode binning function (-> https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/.bincode )

> \# Generating the isopopulation encoded variable: ROE256
> bins_cut = 255
> ROE256 <- .bincode(wcs2train$ROE, quantile(wcs2train$ROE, probs = seq(0, 1, 1/bins_cut), na.rm = TRUE), TRUE)
> \# Generating the Guass Copula encoded variable: ROE256G
> ROE256G <- c()
> ROE256G <- vector(mode="numeric", length(ROE256))
> for(i in 1:length(ROE256)){ <br>
	ROE256G[i] <- tgauss[ROE256[i]+1] <br>
} <br>

> \# Producing an illustration comparing the histograms of ROE256 and ROE256G



