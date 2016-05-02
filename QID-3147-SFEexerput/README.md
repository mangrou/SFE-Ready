
[<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/banner.png" alt="Visit QuantNet">](http://quantlet.de/index.php?p=info)

## [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **SFEexerput** [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/d3/ia)

```yaml

Name of QuantLet : SFEexerput

Published in : Statistics of Financial Markets

Description : 'Calculates the exercise price applying Newton''s method and gets the put option
price using the Black Scholes model.'

Keywords : 'Newton, black-scholes, european-option, exercise-price, financial, option,
option-price, put'

Author : Ying Chen

Submitted : Fri, June 05 2015 by Lukas Borke

Input: 
- t0: Spot Date
- V: Capital
- F: Floor
- T: Expiration Date
- s0: Spot Stock Price
- r: Continuous Interest Rate
- sig: Volatility
- d: Continuous Dividend

Output: 
- k: Exercise Price applying Newton Method
- pk: BS Put Option Price

Example : 'User inputs the parameters [Spot date, Capital, Floor, Expiration date] like [0, 100000,
95000, 2], and [Spot Stock Price, Continuous Interest Rate, Volatility, Continuous Dividend] like
[100, 0.1, 0.3, 0.02] and gets the exercise price 99.56 and the BS put option price 8.72.'

```


```r

# clear variables and close windows
rm(list = ls(all = TRUE))
graphics.off()

# input parameters: Spot date t0, Capital V, Floor F and Expiration date T as vector 
# e.g. [0, 100000, 95000, 2]
para = c(0, 1e+05, 95000, 2)

t0 = para[1]
V  = para[2]
F  = para[3]
T  = para[4]

# input parameters: Spot stock price s0, Interest r, Volatility sig, and Dividend D as vector 
# e.g. [100, 0.1, 0.3, 0.02]
para2 = c(100, 0.1, 0.3, 0.02)

s0  = para2[1]
r   = para2[2]
sig = para2[3]
d   = para2[4]
tau = T - t0    # maturity tau=T-to
b   = r - d     # costs of carry

# main computation: Newton's method
k = 0.001  	# initial exercise price
t = 100  	# initial difference between two ks
while (t >= 1e-05) {
    # acceptable value for difference
    y = (log(s0/k) + (b - 1/2 * (sig^2)) * tau)/(sig * sqrt(tau))       # y for BS 
    yk = -1/(sig * sqrt(tau) * k)                                       # FOC of y respect to k
    cdfnyk1 = -exp(-1 * y^2/2) * (yk/sqrt(2 * pi))                      # FOC of PI(-y) respect to k
    cdfnyk2 = -exp(-1 * (y + sig * sqrt(tau))^2/2) * (yk/sqrt(2 * pi))  # FOC of PI(-y-sig*sqrt(tau))
    
    pk = exp(-r * tau) * k * pnorm(-1 * y) - exp((b - r) * tau) * s0 * pnorm(-1 * 
        y - sig * sqrt(tau))  # BC's put option price 
    pkk = exp(-r * tau) * pnorm(-1 * y) + exp(-1 * r * tau) * k * cdfnyk1 - 
        exp((b - r) * tau) * s0 * cdfnyk2         # FOC of put price respect to k
    fk = exp(-d * tau) * s0 + pk - V/F * k        # equation 2-23 see page 30
    fkk = pkk - V/F                               # FOC of equation respect to k
    k0 = k                                        # old k
    k = k - fk/fkk                                # new k
    t = k - k0                                    # difference 
}

# output
print("The exercise price applying NEWTON method =")
print(k)

print("The BS put option price =")
print(pk) 

```
