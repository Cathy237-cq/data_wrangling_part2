data_wrangling_part2
================
cathy
2024-10-10

load the package need for this one

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(rvest)
```

    ## 
    ## Attaching package: 'rvest'
    ## 
    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

``` r
library(httr)
```

now the data has been imported

``` r
 url = "http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm"

 drug_use_html = read_html(url)
```

Get the pieces i actually need.

``` r
  marj_use_df =
    drug_use_html |> 
    html_table() |> 
    first() |> 
    slice(-1)
```

Learning assessment

``` r
 url = "https://www.bestplaces.net/cost_of_living/city/new_york/new_york"
 cost_living_html = read_html(url)
 
 cost_living_df = 
   cost_living_html |> 
   html_table()
```

also can be combine to one step

``` r
 cost_living_df = 
    read_html("https://www.bestplaces.net/cost_of_living/city/new_york/new_york") |> 
   html_table() |> 
   first() # make first row the name
```
