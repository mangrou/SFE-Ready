
[<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/banner.png" alt="Visit QuantNet">](http://quantlet.de/index.php?p=info)

## [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **SFEclose** [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/d3/ia)

```yaml

Name of QuantLet : SFEclose

Published in : Statistics of Financial Markets

Description : 'Plots the closing stock prices of 4 DAX companies: Bayer (black), BMW (red), Siemens
(blue) and Volkswagen (green) for the period 1 January 2002 - 31 December 2012, on daily basis.'

Keywords : 'asset, data visualization, dax, financial, graphical representation, plot, stock-price,
visualization'

See also : SFEportfolio

Author : Zografia Anastasiadou, Awdesch Melzer

Submitted : Sat, July 18 2015 by quantomas

Datafiles : BAYER_close_0012.dat, BMW_close_0012.dat, SIEMENS_close_0012.dat, VW_close_0012.dat

```

![Picture1](SFEclose-1.png)


```r
# clear variables and close windows
rm(list = ls(all = TRUE))
graphics.off()

x1 = read.table("BAYER_close_0012.dat")
x2 = read.table("BMW_close_0012.dat")
x3 = read.table("SIEMENS_close_0012.dat")
x4 = read.table("VW_close_0012.dat")

x1 = as.matrix(x1)
x2 = as.matrix(x2)
x3 = as.matrix(x3)
x4 = as.matrix(x4)

t = seq(23, dim(x1)[1], by = 261)

plot(x3, type = "l", ylim = c(min(x1, x2, x3, x4), max(x1, x2, x3, x4)), col = "blue3", xlab = "", 
    ylab = "", main = "Closing Prices for German Companies", xaxt = "n")
lines(x1, lty = 2)
lines(x2, col = "red3", lty = 3)
lines(x4, col = "darkgreen", lty = 4)
axis(1, at = t, labels = seq(2000, 2012, 1)) 
```
