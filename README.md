<!-- README.md is generated from README.Rmd. Please edit that file -->
[![Travis-CI Build Status](https://travis-ci.org/earowang/rwalkr.svg?branch=master)](https://travis-ci.org/earowang/rwalkr) [![CRAN\_Status\_Badge](http://www.r-pkg.org/badges/version/rwalkr)](https://cran.r-project.org/package=rwalkr) [![Downloads](http://cranlogs.r-pkg.org/badges/rwalkr?color=brightgreen)](https://cran.r-project.org/package=rwalkr)

rwalkr
======

The goal of **rwalkr** is to provide API to the pedestrian data from the City of Melbourne in tidy data form.

Installation
------------

You could install the stable version from CRAN:

``` r
install.packages("rwalkr")
```

You could install the development version from Github using:

``` r
# install.packages("devtools")
devtools::install_github("earowang/rwalkr")
```

Usage
-----

### `walk_melb()`

The `walk_melb()` function provides API using compedapi, where counts are uploaded on a daily basis. The starting and ending dates inform of which period to be pulled.

``` r
library(rwalkr)
start_date <- as.Date("2017-07-01")
end_date <- start_date + 6L
ped <- walk_melb(from = start_date, to = end_date)
head(ped)
#>                  Sensor  Date_Time       Date Time Count
#> 1         State Library 2017-07-01 2017-07-01    0   334
#> 2 Collins Place (South) 2017-07-01 2017-07-01    0    82
#> 3 Collins Place (North) 2017-07-01 2017-07-01    0    51
#> 4     Flagstaff Station 2017-07-01 2017-07-01    0     0
#> 5     Melbourne Central 2017-07-01 2017-07-01    0   826
#> 6      Town Hall (West) 2017-07-01 2017-07-01    0   682
```

Use *ggplot2* for visualisation:

``` r
library(ggplot2)
ggplot(data = subset(ped, Sensor == "Melbourne Central")) +
  geom_line(aes(x = Date_Time, y = Count))
```

![](man/figure/plot-1.png)

### `run_melb()`

The `run_melb()` function provides API using Socrata, where counts are uploaded on a monthly basis. It should scrape much faster than the function `walk_melb()`.

``` r
run_melb(year = 2016:2017)
```

### `shine_melb()`

The function `shine_melb()` launches a shiny app to give a glimpse of the data. It provides two basic plots: one is an overlaying time series plot, and the other is a dot plot indicating missing values. Below is a screen-shot of the shiny app.

![](man/figure/shiny.png)
