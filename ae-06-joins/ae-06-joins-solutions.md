AE-06: Joins practice - Solutions
================

``` r
library(tidyverse)
library(skimr)
```

The `dplyr` packages contains a few small datasets that are useful for
understanding how different joins work.

First look at the dataframes:

``` r
band_members
```

    ## # A tibble: 3 × 2
    ##   name  band   
    ##   <chr> <chr>  
    ## 1 Mick  Stones 
    ## 2 John  Beatles
    ## 3 Paul  Beatles

``` r
band_instruments
```

    ## # A tibble: 3 × 2
    ##   name  plays 
    ##   <chr> <chr> 
    ## 1 John  guitar
    ## 2 Paul  bass  
    ## 3 Keith guitar

In groups, take turns coding and interpreting the output. One person
should try to figure out and run the code. The other person (or people)
should look at the output and put into words what the code does.

1.  Combine `band_members` and `band_instruments` using `left_join`.
    Explain in your own words what happened. How does R handle rows that
    contain data in x but not y?

<!-- end list -->

``` r
band_members %>%
  left_join(band_instruments)
```

    ## Joining, by = "name"

    ## # A tibble: 3 × 3
    ##   name  band    plays 
    ##   <chr> <chr>   <chr> 
    ## 1 Mick  Stones  <NA>  
    ## 2 John  Beatles guitar
    ## 3 Paul  Beatles bass

*We combined the `band_members` dataframe with the `band_instruments`
dataframe based on common values in the `name` column. With `left_join`,
rows contained in `band_members` (x) are included in the output. Rows
that are in `band_instruments` (y) but not `band_members` are not
included in the output. Essentially, these rows are being filtered out,
so this can be considered a “filtering join.” When rows contain data in
`band_members` but not `band_instruments`, an NA is created (e.g., Mick
is not included in the `band_instruments` dataframe, so an NA is created
in that row in the output).*

2.  Combine `band_members` and `band_instruments` using `right_join`.
    Explain in your own words what happened.

<!-- end list -->

``` r
band_members %>%
  right_join(band_instruments)
```

    ## Joining, by = "name"

    ## # A tibble: 3 × 3
    ##   name  band    plays 
    ##   <chr> <chr>   <chr> 
    ## 1 John  Beatles guitar
    ## 2 Paul  Beatles bass  
    ## 3 Keith <NA>    guitar

*The opposite as what happened above - with `right_join`, rows contained
in `band_instruments` (y) are included in the output. Rows that are in
`band_members` (x) but not `band_instruments` are not included in the
output.*

3.  Combine `band_members` and `band_instruments` using `full_join`.
    Explain in your own words what happened.

<!-- end list -->

``` r
band_members %>%
  full_join(band_instruments)
```

    ## Joining, by = "name"

    ## # A tibble: 4 × 3
    ##   name  band    plays 
    ##   <chr> <chr>   <chr> 
    ## 1 Mick  Stones  <NA>  
    ## 2 John  Beatles guitar
    ## 3 Paul  Beatles bass  
    ## 4 Keith <NA>    guitar

*The dataframes were combined based on values in the `name` column but
all possible names were included in the output.*

4.  Combine `band_members` and `band_instruments` using `inner_join`.
    Explain in your own words what happened.

<!-- end list -->

``` r
band_members %>%
  inner_join(band_instruments)
```

    ## Joining, by = "name"

    ## # A tibble: 2 × 3
    ##   name  band    plays 
    ##   <chr> <chr>   <chr> 
    ## 1 John  Beatles guitar
    ## 2 Paul  Beatles bass

*The dataframes were combined based on values in the `name` column but
only rows with names contained in BOTH `band_members` and
`band_instruments` were included in the output.*

5.  Combine `band_members` and `band_instruments` using `semi_join`.
    Explain in your own words what happened. Note the column names and
    number of columns - which dataframe are these from?

<!-- end list -->

``` r
band_members %>%
  semi_join(band_instruments)
```

    ## Joining, by = "name"

    ## # A tibble: 2 × 2
    ##   name  band   
    ##   <chr> <chr>  
    ## 1 John  Beatles
    ## 2 Paul  Beatles

*The dataframes were combined based on values in the `name` column. Only
rows with names contained in BOTH `band_members` and `band_instruments`
were included in the output, and only columns in the `band_members`
dataframe were included. Basically, we filtered `band_members` so that
the output only has names contained in `band_instruments`.*

6.  Combine `band_members` and `band_instruments` using `semi_join` but
    reverse the order in which you join them (i.e., if you typed
    `band_members` first and `band_instruments` second in the previous
    chunk, type `band_instruments` first this time). Explain in your own
    words what happened. Note the column names and number of columns -
    which dataframe are these from?

<!-- end list -->

``` r
band_instruments %>%
  semi_join(band_members)
```

    ## Joining, by = "name"

    ## # A tibble: 2 × 2
    ##   name  plays 
    ##   <chr> <chr> 
    ## 1 John  guitar
    ## 2 Paul  bass

*The dataframes were combined based on values in the `name` column. Only
rows with names contained in BOTH `band_members` and `band_instruments`
were included in the output, and only columns in the `band_instruments`
dataframe were included. Basically, we filtered `band_instruments` so
that the output only has names contained in `band_members`.*

7.  Combine `band_members` and `band_instruments` using `anti_join`.
    Explain in your own words what happened. Note the column names and
    number of columns - which dataframe are these from?

<!-- end list -->

``` r
band_members %>%
  anti_join(band_instruments)
```

    ## Joining, by = "name"

    ## # A tibble: 1 × 2
    ##   name  band  
    ##   <chr> <chr> 
    ## 1 Mick  Stones

*The dataframes were combined based on values in the `name` column. Only
rows with names contained in NEITHER `band_members` nor
`band_instruments` were included in the output, and only columns in the
`band_members` dataframe were included. Basically, we filtered
`band_members` so that the output only has names that are not contained
in `band_instruments`.*

8.  Combine `band_members` and `band_instruments` using `anti_join` but
    reverse the order in which you join them (i.e., if you typed
    `band_members` first and `band_instruments` second in the previous
    chunk, type `band_instruments` first this time). Explain in your own
    words what happened. Note the column names and number of columns -
    which dataframe are these from?

<!-- end list -->

``` r
band_instruments %>%
  anti_join(band_members)
```

    ## Joining, by = "name"

    ## # A tibble: 1 × 2
    ##   name  plays 
    ##   <chr> <chr> 
    ## 1 Keith guitar

*The dataframes were combined based on values in the `name` column. Only
rows with names contained in NEITHER `band_members` nor
`band_instruments` were included in the output, and only columns in the
`band_instruments` dataframe were included. Basically, we filtered
`band_instruments` so that the output only has names that are not
contained in `band_members`.*
