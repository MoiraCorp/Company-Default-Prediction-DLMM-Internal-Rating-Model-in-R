## LDA on decorrelated variables using a prior PCA

We start by performing a Principal Componenet Analysis (PCA) on the training data table:

> library(stats) <br>
> w <- na.omit(wcs2train.ratios) <br>
> \# Performing a Principal Component Analysis (PCA) <br>
> pca <- prcomp(w, center = TRUE, scale = TRUE) <br>
> \# Building the data table for the LDA on PCA components. <br>
> w.proj <- predict(pca, newdata=w)
> \# Setting the number of PCA components to be used <br>
> nbpcacomp = 7 <br>
> varcount = 0 <br>
>   for(i in 1:nbpcacomp){ <br>
	varcount = varcount + 1 <br>
	if(varcount == 1){ varlist <- c(paste("PC", varcount, sep="")) <br>
	} else { <br>
	  varlist <- append(varlist, paste("PC", varcount, sep="")) <br>
	} <br>
} <br>

Then, we project the data vectors onto the first PCA componenets and perform LDA on this one dimensional dataset.

> \# Selecting the first nbpcacomp PCA components  <br>
> w.pca <- subset(as.data.frame(w.proj),select=varlist) <br>
> w <- na.omit(wcs2trainL) <br>
> wcs2train.pcaL <- cbind(w$BADGOOD, w.pca) <br>
> names(wcs2train.pcaL)[1] = "BADGOOD" <br>
> z <- lda(BADGOOD ~ ., data=wcs2train.pcaL, prior = c(1,1)/2, CV = TRUE) <br>
> table(wcs2train.pcaL$BADGOOD, z$class)


