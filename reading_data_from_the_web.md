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

## CSS Selectors!!

``` r
 swm_url = "https://www.imdb.com/list/ls070150896/"

 swm_html = read_html(swm_url)
```

``` r
swm_title_vec = 
 swm_html |> 
  html_elements(".ipc-title-link-wrapper.ipc-title__text") |> 
  html_text()

swm_runtime_vec = 
 swm_html |> 
  html_elements(".dli-title-metadata-item:nth-child(2)") |> 
  html_text()
 
 swm_score_vec = 
  swm_html |> 
  html_elements(".ipc-rating-star--rating") |> 
  html_text()
```

## Use API

get water data

``` r
 nyc_water = 
   GET("https://data.cityofnewyork.us/resource/ia2d-e54m.csv") |> 
   content() # show as a table
```

    ## Rows: 45 Columns: 4
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## dbl (4): year, new_york_city_population, nyc_consumption_million_gallons_per...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

Get BRFSS data

``` r
 BRFSS_df = 
  GET("https://chronicdata.cdc.gov/resource/acme-vg9e.csv",
      query = list("$limit" = 5000)) |>  # increase the row to 5000, or it will only have 1000
 content()
```

    ## Rows: 5000 Columns: 23
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (16): locationabbr, locationdesc, class, topic, question, response, data...
    ## dbl  (6): year, sample_size, data_value, confidence_limit_low, confidence_li...
    ## lgl  (1): locationid
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

Pokemon API

``` r
 pokemon = 
  GET("https://pokeapi.co/api/v2/pokemon/ditto") |> 
  content()
```

``` r
pokemon$height
```

    ## [1] 3

``` r
pokemon$abilities
```

    ## [[1]]
    ## [[1]]$ability
    ## [[1]]$ability$name
    ## [1] "limber"
    ## 
    ## [[1]]$ability$url
    ## [1] "https://pokeapi.co/api/v2/ability/7/"
    ## 
    ## 
    ## [[1]]$is_hidden
    ## [1] FALSE
    ## 
    ## [[1]]$slot
    ## [1] 1
    ## 
    ## 
    ## [[2]]
    ## [[2]]$ability
    ## [[2]]$ability$name
    ## [1] "imposter"
    ## 
    ## [[2]]$ability$url
    ## [1] "https://pokeapi.co/api/v2/ability/150/"
    ## 
    ## 
    ## [[2]]$is_hidden
    ## [1] TRUE
    ## 
    ## [[2]]$slot
    ## [1] 3
