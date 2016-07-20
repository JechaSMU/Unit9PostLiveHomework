# UK Cars Forcasting
Jean Jecha  
July 18, 2016  


#### Time series plot for UK Cars
  * Upward trend from 1985 to 2005
  * Not an identifiable seasonal trend

```r
# Get cars dataset
data(ukcars)
# regular time series plot
plot(ukcars)
```

![](UKCarsForcasting_files/figure-html/get.cars-1.png)<!-- -->

#### Classical Decomposition Trend
  * More smoother upward trend from 1985 to 2005
  * Seasonal trend more identifiable
  * Looks like the low is in the beginning of the year

```r
# Classical decomposition to calculate trend cycle
fitd <- decompose(ukcars)
plot(fitd)
```

![](UKCarsForcasting_files/figure-html/decompose.cars-1.png)<!-- -->

####  Seasonally adjusted plot
  * Less of an extreme in seasonal trend
  * still shows the upward trend

```r
# Seasonally adjusted data
ukcadj <- seasadj(fitd)
plot(ukcadj)
```

![](UKCarsForcasting_files/figure-html/seas.adj.cars-1.png)<!-- -->

####  Normal Time-Series plot using TS
  * Seeing the upward trend from 1985 to 2005

```r
ukcars2 <- ts(ukcars,start=c(1977,1),frequency=4)
plot(ukcars2)
```

![](UKCarsForcasting_files/figure-html/ts.cars-1.png)<!-- -->

#### Time-Series plot with middle outlier
  * Changes the range compare to without outlier
  * Overall trend is there but not a pronounced


```r
# plot outlier in middle
ukcars3 <- ts(c(ukcars[1:50],ukcars[55]+300,ukcars[51:113]),start=c(1977,1),frequency=4)
plot(ukcars3)
```

![](UKCarsForcasting_files/figure-html/ts.cars.middle.outlier-1.png)<!-- -->

#### Time-Series plot with end outlier
  * Very similar to the plot with the middle outlier
  * Trend is the same showing the high peak at the end instead of middle

```r
# plot outlier end
ukcars4 <- ts(c(ukcars[1:113],ukcars[55]+300),start=c(1977,1),frequency=4)
plot(ukcars4)
```

![](UKCarsForcasting_files/figure-html/ts.cars.end.outlier-1.png)<!-- -->

#### Using STL Decompose series
  * Trend is same with classical decompose
  * Seasonal is similar as classical decompose
  * Data and observed seem the same
  * Contains a remainder plot then the classical decompose

```r
# Use STL for decompose
ukcstl <- stl(ukcars, s.window="periodic")
plot(ukcstl)
```

![](UKCarsForcasting_files/figure-html/stl.cars-1.png)<!-- -->

#### Showing regular plot data with the time series trend

```r
# plot regular data with time series trend from stl
plot(ukcars, col="gray",
     main="UK Cars",
     ylab="New orders index", xlab="")
lines(ukcstl$time.series[,2],col="red",ylab="Trend")
```

![](UKCarsForcasting_files/figure-html/cars.series.trend-1.png)<!-- -->

