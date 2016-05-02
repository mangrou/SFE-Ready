
[<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/banner.png" alt="Visit QuantNet">](http://quantlet.de/index.php?p=info)

## [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **SFENormalApprox4** [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/d3/ia)

```yaml

Name of QuantLet : SFENormalApprox4

Published in : Statistics of Financial Markets

Description : 'Computes numerical approximation to a normal cumulative distribution function (cdf)
using method d).'

Keywords : 'approximation, cdf, distribution, graphical representation, normal,
normal-distribution, numeric, plot'

See also : SFENormalApprox1, SFENormalApprox1, SFENormalApprox2, SFENormalApprox3, SFENormalApprox3

Author : Wolfgang K. Haerdle

Submitted : Fri, July 17 2015 by quantomas

Output: 
- phi: approximation of Normal cdf at different values

Example : 'Estimated normal cdf at that points 1:0.1:2 are given: [0.8413 0.8643 0.8849 0.9032
0.9192 0.9332 0.9452 0.9554 0.9641 0.9713 0.9772].'

```

![Picture1](SFENormalApprox4-1.png)


```r
rm(list = ls(all = TRUE))
graphics.off()

# install and load packages
libraries = c("gplots")
lapply(libraries, function(x) if (!(x %in% installed.packages())) {
  install.packages(x)
})
lapply(libraries, library, quietly = TRUE, character.only = TRUE)

# main computation
y   = seq(1, 2, 0.1)   # estimation points
k   = 10               # order number 
n   = 0
sum	= 0
while (n < (k + 1)) {
    sum = sum + ((-1)^n) * y^(2 * n + 1)/(factorial(n) * 2^n * (2 * n + 1))
    n	= n + 1
}
phi = 0.5 + sum/sqrt(2 * pi)

# output
print("Estimation Points")
print(y)
print("Estimated Normal CDF")
print(phi)

# plot
par(mfrow = c(1, 2))
plot(y, phi, lwd = 2, xlab = "x", type = "o", ylab = "cdf", main = "Approximation to normal cdf d", col = "blue3")
textplot(cbind(y, phi)) 
```
