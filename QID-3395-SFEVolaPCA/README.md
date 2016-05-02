
[<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/banner.png" alt="Visit QuantNet">](http://quantlet.de/index.php?p=info)

## [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **SFEVolaPCA** [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/d3/ia)

```yaml

Name of QuantLet : SFEVolaPCA

Published in : Statistics of Financial Markets

Description : 'Calculates the explained sample variance and the cumulative variance using principal
components (in percentages).'

Keywords : dax, financial, implied-volatility, pca, variance, vdax, volatility

See also : SFEVolSurfPlot, SFEVolSurfPlot, SFEVolaCov, SFEVolaTermStructure

Author : Joanna Tomanek

Submitted : Fri, July 17 2015 by quantomas

Datafiles : implvola.dat

```


```r
# clear variables and close windows
rm(list = ls(all = TRUE))
graphics.off()

# load data
x = read.table("implvola.dat")

# rescale
x = x * 100

# number of rows
n = nrow(x)

# calculate first differences
z=apply(x,2,diff)

# calculate covariance
s = cov(z) * 1e+05

# calculate eigenvalues and eigenvectors
e = eigen(s, symmetric = TRUE)
l = e$values

# percentage of explained variance
l/sum(l) * 100

# cumulative sum of percentage of explained variance
cumsum(l/sum(l) * 100) 
```
