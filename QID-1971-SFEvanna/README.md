
[<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/banner.png" alt="Visit QuantNet">](http://quantlet.de/index.php?p=info)

## [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **SFEvanna** [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/d3/ia)

```yaml

Name of QuantLet : SFEvanna

Published in : Statistics of Financial Markets

Description : 'Plots the Vanna of a call option as a function of the time to maturity and the asset
price.'

Keywords : 'asset, black-scholes, call, european-option, financial, graphical representation,
greeks, option, option-price, plot'

See also : 'SFEvolga, SFEdelta, SFEgamma, SFEvega, SFEtheta, SFEspeed, SFEcharmcall, SFEcolor,
SFEultima, SFEvomma, SFEzomma, SFEdvegadtime'

Author : Andreas Golle, Awdesch Melzer

Submitted : Tue, June 17 2014 by Franziska Schulz

Example : 'For given [lower, upper] bound of Asset price S like [50,150] and [lower, upper] bound
of time to maturity tau like [0.05, 1] a plot of the Theta of a call option is produced.'

```

![Picture1](SFEvanna-1.png)


```r

# clear variables and close windows
rm(list = ls(all = TRUE))
graphics.off()

# install and load packages
libraries = c("lattice")
lapply(libraries, function(x) if (!(x %in% installed.packages())) {
install.packages(x)
})
lapply(libraries, library, quietly = TRUE, character.only = TRUE)

# parameter settings
# parameter settings
S_min   = 50          # lower bound of Asset Price
S_max   = 150         # upper bound of Asset Price 
tau_min = 0.01        # lower bound of Time to Maturity
tau_max = 1           # upper bound of Time to Maturity
k       = 100         # exercise price 
r       = 0           # interest rate
sig     = 0.25        # volatility
tau     = 0.5         # time to maturity
q       = 0           # dividend rate
b       = r - q       # cost of carry
steps   = 100         # steps

meshgrid = function(a, b) {
    list(x = outer(b * 0, a, FUN = "+"), y = outer(b, a * 0, FUN = "+"))
}

first = meshgrid(seq(tau_min, tau_max, -(tau_min - tau_max)/(steps - 1)), seq(tau_min, tau_max, -(tau_min - tau_max)/(steps - 
    1)))

tau  = first$x
dump = first$y

second = meshgrid(seq(S_min, S_max, -(S_min - S_max)/(steps - 1)), seq(S_min, S_max, -(S_min - S_max)/(steps - 1)))

dump2 = second$x
S     = second$y

d1    = (log(S/k) + (r - q - sig^2/2) * tau)/(sig * sqrt(tau))
d2    = d1 - sig * sqrt(tau)
Vanna = -(exp((b - r) * tau) * d2)/sig * dnorm(d1)

# Plot
title = bquote(expression(paste("Strike price is ", .(k), ", interest rate is ", 
    .(r), ", dividend rate is ", .(q), ", annual volatility is ", .(sig))))
wireframe(Vanna ~ tau * S, drape = T, ticktype = "detailed", main = expression(paste("Vanna as function of the time to maturity ", 
    tau, " and the asset price S")), sub = title, scales = list(arrows = FALSE, 
    col = "black", distance = 1, tick.number = 8, cex = 0.7, x = list(labels = round(seq(tau_min, 
        tau_max, length = 11), 1)), y = list(labels = round(seq(S_min, S_max, length = 11), 
        1))), xlab = list(expression(paste("Time to Maturity  ", tau)), rot = 30, 
    cex = 1.2), ylab = list("Asset Price S", rot = -40, cex = 1.2), zlab = list("Vanna", 
    cex = 1.1))

```
