# TCP Stock Forcasting
Jean Jecha  
July 20, 2016  


```r
#install.packages("tseries")
library(tseries)
```

```r
SNPdata <- get.hist.quote('TCP',quote="Close")
```

```
## time series starts 1999-05-25
```

```r
SNPret <- log(lag(SNPdata)) - log(SNPdata)
SNPvol <- sd(SNPret) * sqrt(250) * 100
```


```r
## volatility
Vol <- function(d, logrets)
{
  var = 0
  lam = 0
  varlist <- c()
  for (r in logrets) {
    lam = lam*(1 - 1/d) + 1
    var = (1 - 1/lam)*var + (1/lam)*r^2
    varlist <- c(varlist, var)
  }
  sqrt(varlist)
}
```

```r
# Recreate Figure 6.12 in the text on page 155
volest <- Vol(10,SNPret)
volest2 <- Vol(30,SNPret)
volest3 <- Vol(100,SNPret)
```

```r
plot(volest,type="l")
lines(volest2,type="l",col="red")
lines(volest3, type = "l", col="blue")
```

![](StockForcasting_files/figure-html/volPlot-1.png)<!-- -->
