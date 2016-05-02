
[<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/banner.png" alt="Visit QuantNet">](http://quantlet.de/index.php?p=info)

## [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **SFEcir** [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/d3/ia)

```yaml

Name of QuantLet : SFEcir

Published in : Statistics of Financial Markets

Description : 'Displays the yield curve for given parameters under the model of Cox-Ingersoll-Ross
(CIR).'

Keywords : 'cir, graphical representation, interest-rate, plot, process, short-rate, simulation,
time-series, yield, term structure'

See also : SFECIRmle, SFEscomCIR, SFEsimCIR, SFEcirpricing, SFEsimVasi

Author : Joanna Tomanek, Christian M. Hafner

Submitted : Fri, June 13 2014 by Felix Jung

```

![Picture1](SFEcir-1.png)


```r

# clear variables and close windows
rm(list = ls(all = TRUE))
graphics.off()

# parameter settings
r   = 1
k   = 0.1   # reversion rate
mu  = 0.1   # steady state of the short rate
s   = 0.1   # volatility coefficient
n   = 50    # time horizon in years
sr  = 0.05  # today's short rate
tau = 1:n   # vector of maturities in years

if (s == 0) {
    print("Specify Volatility other than zero!")
}

if (k < 0) {
    print("Mean reversion rate should be non-negative!")
}

gam  = sqrt(k^2 + 2 * s^2)
ylim = 2 * k * mu/(gam + k)
g    = 2 * gam + (k + gam) * (exp(gam * tau) - 1)
b    = -(2 * (exp(gam * tau) - 1))/g
a    = 2 * k * mu/s^2 * log(2 * gam * exp((k + gam) * tau/2)/g)
p    = exp(a + b * sr)    # the bond prices
y    = (-1/tau) * log(p)  # the yields
w    = cbind(tau, y)
wlim = cbind(tau, (matrix(1, n, 1) * ylim))
nn   = c(1, 50)
mm   = c(min(wlim[, 2], w[, 2]), max(wlim[, 2], w[, 2]))

# plot
plot(nn, mm, type = "n", main = "Yield Curve, Cox/Ingersoll/Ross Model", xlab = "Time to Maturity", 
    ylab = "Yield")
lines(w, col = 4, lwd = 2)
lines(wlim, col = 2, lwd = 2)

z = cbind(tau, p, y)
list(z = z, ylim = ylim)
```
