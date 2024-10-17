strings and factors
================

load the package need for this one

``` r
library(rvest)
```

    ## 
    ## Attaching package: 'rvest'

    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

## Let’s do strings

``` r
string_vec = c("my", "name", "is", "cathy")

str_detect(string_vec, "cathy") # need to have percice match, upper case and lower case
```

    ## [1] FALSE FALSE FALSE  TRUE

``` r
str_replace(string_vec, "cathy", "Cahty")
```

    ## [1] "my"    "name"  "is"    "Cahty"

``` r
str_replace(string_vec, "a", "A")
```

    ## [1] "my"    "nAme"  "is"    "cAthy"

``` r
string_vec = c(
  "i think we all rule for participating",
  "i think i have been caught",
  "i think this will be quite fun actually",
  "it will be fun, i think"
  )

str_detect(string_vec, "i think")
```

    ## [1] TRUE TRUE TRUE TRUE

``` r
str_detect(string_vec, "^i think") # ^ beginning of the line  with "i think"
```

    ## [1]  TRUE  TRUE  TRUE FALSE

``` r
str_detect(string_vec, "^i think$")  # $ end with "i think"
```

    ## [1] FALSE FALSE FALSE FALSE

``` r
string_vec = c(
  "Time for a Pumpkin Spice Latte!",
  "went to the #pumpkinpatch last weekend",
  "Pumpkin Pie is obviously the best pie",
  "SMASHING PUMPKINS -- LIVE IN CONCERT!!"
  )

str_detect(string_vec,"pumpkin")
```

    ## [1] FALSE  TRUE FALSE FALSE

``` r
str_detect(string_vec,"Pumpkin")
```

    ## [1]  TRUE FALSE  TRUE FALSE

``` r
str_detect(string_vec,"[Pp]umpkin") # can find 2 types of P and p 
```

    ## [1]  TRUE  TRUE  TRUE FALSE

``` r
string_vec = c(
  '7th inning stretch',
  '1st half soon to begin. Texas won the toss.',
  'she is 5 feet 4 inches tall',
  '3AM - cant sleep :('
  )

str_detect(string_vec, "[0-9]")
```

    ## [1] TRUE TRUE TRUE TRUE

``` r
str_detect(string_vec, "[0-9][a-z]")
```

    ## [1]  TRUE  TRUE FALSE FALSE

``` r
str_detect(string_vec, "^[0-9][a-zA-Z]")
```

    ## [1]  TRUE  TRUE FALSE  TRUE

``` r
string_vec = c(
  'Its 7:11 in the evening',
  'want to go to 7-11?',
  'my flight is AA711',
  'NetBios: scanning ip 203.167.114.66'
  )

str_detect(string_vec, "7.11") # "." means everything
```

    ## [1]  TRUE  TRUE FALSE  TRUE

how thing start get real strange

``` r
string_vec = c(
  'The CI is [2, 5]',
  ':-]',
  ':-[',
  'I found the answer on pages [6-7]'
  )

str_detect(string_vec, "\\[")
```

    ## [1]  TRUE FALSE  TRUE  TRUE

## Factors …

``` r
sex_vec = factor(c("male","male","female","female"))

as.numeric(sex_vec)
```

    ## [1] 2 2 1 1

do some releveling

``` r
sex_vec = fct_relevel(sex_vec, "male") # put male first

as.numeric(sex_vec)
```

    ## [1] 1 1 2 2
