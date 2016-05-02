
[<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/banner.png" alt="Visit QuantNet">](http://quantlet.de/index.php?p=info)

## [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **SFEhillquantile** [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/d3/ia)

```yaml

Name of QuantLet : SFEhillquantile

Published in : Statistics of Financial Markets

Description : Estimates the Hill-quantile value given a Hill-estimation of gamma.

Keywords : 'VaR, distribution, estimation, extreme-value, forecast, generalized-pareto-model,
hill-estimator, pareto, quantile, risk, standard'

Author : Joanna Tomanek

Submitted : Thu, July 16 2015 by quantomas

```


```r
# clear variables and close windows
rm(list = ls(all = TRUE))
graphics.off()

# install and load packages
libraries = c("fExtremes")
lapply(libraries, function(x) if (!(x %in% installed.packages())) {
    install.packages(x)
})
lapply(libraries, library, quietly = TRUE, character.only = TRUE)

# Main computation
x = rgpd(100, xi = 0.1)  # generate a generalized pareto distributed variables 
x = sort(x)
n = length(x)
q = "0.01"
k = "10"

message = "      Quantile"
default = q
q = winDialogString(message, default)
q = type.convert(q, na.strings = "NA", as.is = FALSE, dec = ".")

message = "      Excess"
default = k
k = winDialogString(message, default)
k = type.convert(k, na.strings = "NA", as.is = FALSE, dec = ".")

if (k < 8 && k > (n - 1)) warning("SFEhillquantile: excess should be greater than 8 and less than the number of elements.", 
    call. = FALSE)
if (q < 0 && q > 1) warning("SFEhillquantile: please give a rational quantile value.", 
    call. = FALSE)

rest = gpdFit(x, nextremes = k, type = "mle")				# ML-estimation of gamma 
rest = rest@parameter

# the Hill-quantile value
(xest = x[k] + x[k] * (((n/k) * (1 - q))^(-rest$u) - 1))	# Hill-quantil estimation
```
