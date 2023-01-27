`dplyr` code-along
================
1/30/2023

These are some of the many `dplyr` functions:

  - `select`: pick columns by name
  - `arrange`: reorder rows
  - `slice`: pick rows using index(es)
  - `filter`: pick rows matching criteria
  - `distinct`: find unique observations
  - `mutate`: add new variables
  - `summarize`: reduce variables to values
  - `group_by`: used for a variety of grouped operations

<!-- end list -->

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
    ## ✔ ggplot2 3.3.6     ✔ purrr   1.0.1
    ## ✔ tibble  3.1.8     ✔ dplyr   1.0.7
    ## ✔ tidyr   1.1.4     ✔ stringr 1.5.0
    ## ✔ readr   2.1.1     ✔ forcats 0.5.1
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
library(palmerpenguins)
```

Let’s code the following together using the `penguins` dataset to give
you practice using pipes and some of these `dplyr` functions:

### 1\. Select `species`, `bill_length_mm`, and `year`

``` r
penguins %>%
  select(species, bill_length_mm, year)
```

    ## # A tibble: 344 × 3
    ##    species bill_length_mm  year
    ##    <fct>            <dbl> <int>
    ##  1 Adelie            39.1  2007
    ##  2 Adelie            39.5  2007
    ##  3 Adelie            40.3  2007
    ##  4 Adelie            NA    2007
    ##  5 Adelie            36.7  2007
    ##  6 Adelie            39.3  2007
    ##  7 Adelie            38.9  2007
    ##  8 Adelie            39.2  2007
    ##  9 Adelie            34.1  2007
    ## 10 Adelie            42    2007
    ## # … with 334 more rows

``` r
#or

select(penguins, c(species, bill_length_mm, year))
```

    ## # A tibble: 344 × 3
    ##    species bill_length_mm  year
    ##    <fct>            <dbl> <int>
    ##  1 Adelie            39.1  2007
    ##  2 Adelie            39.5  2007
    ##  3 Adelie            40.3  2007
    ##  4 Adelie            NA    2007
    ##  5 Adelie            36.7  2007
    ##  6 Adelie            39.3  2007
    ##  7 Adelie            38.9  2007
    ##  8 Adelie            39.2  2007
    ##  9 Adelie            34.1  2007
    ## 10 Adelie            42    2007
    ## # … with 334 more rows

### 2\. Select `species`, `bill_length_mm`, and `year` and then arrange by `bill_length_mm`

``` r
penguins %>%
  select(species, bill_length_mm, year) %>%
  arrange(bill_length_mm)
```

    ## # A tibble: 344 × 3
    ##    species bill_length_mm  year
    ##    <fct>            <dbl> <int>
    ##  1 Adelie            32.1  2009
    ##  2 Adelie            33.1  2008
    ##  3 Adelie            33.5  2008
    ##  4 Adelie            34    2008
    ##  5 Adelie            34.1  2007
    ##  6 Adelie            34.4  2007
    ##  7 Adelie            34.5  2008
    ##  8 Adelie            34.6  2007
    ##  9 Adelie            34.6  2008
    ## 10 Adelie            35    2008
    ## # … with 334 more rows

### 3\. Filter the `penguins` dataset to only keep observations from 2007

``` r
penguins %>%
  filter(year == 2007)
```

    ## # A tibble: 110 × 8
    ##    species island    bill_length_mm bill_depth_mm flipper_…¹ body_…² sex    year
    ##    <fct>   <fct>              <dbl>         <dbl>      <int>   <int> <fct> <int>
    ##  1 Adelie  Torgersen           39.1          18.7        181    3750 male   2007
    ##  2 Adelie  Torgersen           39.5          17.4        186    3800 fema…  2007
    ##  3 Adelie  Torgersen           40.3          18          195    3250 fema…  2007
    ##  4 Adelie  Torgersen           NA            NA           NA      NA <NA>   2007
    ##  5 Adelie  Torgersen           36.7          19.3        193    3450 fema…  2007
    ##  6 Adelie  Torgersen           39.3          20.6        190    3650 male   2007
    ##  7 Adelie  Torgersen           38.9          17.8        181    3625 fema…  2007
    ##  8 Adelie  Torgersen           39.2          19.6        195    4675 male   2007
    ##  9 Adelie  Torgersen           34.1          18.1        193    3475 <NA>   2007
    ## 10 Adelie  Torgersen           42            20.2        190    4250 <NA>   2007
    ## # … with 100 more rows, and abbreviated variable names ¹​flipper_length_mm,
    ## #   ²​body_mass_g

``` r
#or

filter(penguins, year == 2007)
```

    ## # A tibble: 110 × 8
    ##    species island    bill_length_mm bill_depth_mm flipper_…¹ body_…² sex    year
    ##    <fct>   <fct>              <dbl>         <dbl>      <int>   <int> <fct> <int>
    ##  1 Adelie  Torgersen           39.1          18.7        181    3750 male   2007
    ##  2 Adelie  Torgersen           39.5          17.4        186    3800 fema…  2007
    ##  3 Adelie  Torgersen           40.3          18          195    3250 fema…  2007
    ##  4 Adelie  Torgersen           NA            NA           NA      NA <NA>   2007
    ##  5 Adelie  Torgersen           36.7          19.3        193    3450 fema…  2007
    ##  6 Adelie  Torgersen           39.3          20.6        190    3650 male   2007
    ##  7 Adelie  Torgersen           38.9          17.8        181    3625 fema…  2007
    ##  8 Adelie  Torgersen           39.2          19.6        195    4675 male   2007
    ##  9 Adelie  Torgersen           34.1          18.1        193    3475 <NA>   2007
    ## 10 Adelie  Torgersen           42            20.2        190    4250 <NA>   2007
    ## # … with 100 more rows, and abbreviated variable names ¹​flipper_length_mm,
    ## #   ²​body_mass_g

### 4\. Filter the `penguins` dataset to only keep observations after 2007

``` r
penguins %>%
  filter(year > 2007)
```

    ## # A tibble: 234 × 8
    ##    species island bill_length_mm bill_depth_mm flipper_len…¹ body_…² sex    year
    ##    <fct>   <fct>           <dbl>         <dbl>         <int>   <int> <fct> <int>
    ##  1 Adelie  Biscoe           39.6          17.7           186    3500 fema…  2008
    ##  2 Adelie  Biscoe           40.1          18.9           188    4300 male   2008
    ##  3 Adelie  Biscoe           35            17.9           190    3450 fema…  2008
    ##  4 Adelie  Biscoe           42            19.5           200    4050 male   2008
    ##  5 Adelie  Biscoe           34.5          18.1           187    2900 fema…  2008
    ##  6 Adelie  Biscoe           41.4          18.6           191    3700 male   2008
    ##  7 Adelie  Biscoe           39            17.5           186    3550 fema…  2008
    ##  8 Adelie  Biscoe           40.6          18.8           193    3800 male   2008
    ##  9 Adelie  Biscoe           36.5          16.6           181    2850 fema…  2008
    ## 10 Adelie  Biscoe           37.6          19.1           194    3750 male   2008
    ## # … with 224 more rows, and abbreviated variable names ¹​flipper_length_mm,
    ## #   ²​body_mass_g

``` r
#or

filter(penguins, year > 2007)
```

    ## # A tibble: 234 × 8
    ##    species island bill_length_mm bill_depth_mm flipper_len…¹ body_…² sex    year
    ##    <fct>   <fct>           <dbl>         <dbl>         <int>   <int> <fct> <int>
    ##  1 Adelie  Biscoe           39.6          17.7           186    3500 fema…  2008
    ##  2 Adelie  Biscoe           40.1          18.9           188    4300 male   2008
    ##  3 Adelie  Biscoe           35            17.9           190    3450 fema…  2008
    ##  4 Adelie  Biscoe           42            19.5           200    4050 male   2008
    ##  5 Adelie  Biscoe           34.5          18.1           187    2900 fema…  2008
    ##  6 Adelie  Biscoe           41.4          18.6           191    3700 male   2008
    ##  7 Adelie  Biscoe           39            17.5           186    3550 fema…  2008
    ##  8 Adelie  Biscoe           40.6          18.8           193    3800 male   2008
    ##  9 Adelie  Biscoe           36.5          16.6           181    2850 fema…  2008
    ## 10 Adelie  Biscoe           37.6          19.1           194    3750 male   2008
    ## # … with 224 more rows, and abbreviated variable names ¹​flipper_length_mm,
    ## #   ²​body_mass_g

### 5\. Filter the `penguins` dataset to only keep observations from `Dream` island

``` r
penguins %>%
  filter(island == "Dream")
```

    ## # A tibble: 124 × 8
    ##    species island bill_length_mm bill_depth_mm flipper_len…¹ body_…² sex    year
    ##    <fct>   <fct>           <dbl>         <dbl>         <int>   <int> <fct> <int>
    ##  1 Adelie  Dream            39.5          16.7           178    3250 fema…  2007
    ##  2 Adelie  Dream            37.2          18.1           178    3900 male   2007
    ##  3 Adelie  Dream            39.5          17.8           188    3300 fema…  2007
    ##  4 Adelie  Dream            40.9          18.9           184    3900 male   2007
    ##  5 Adelie  Dream            36.4          17             195    3325 fema…  2007
    ##  6 Adelie  Dream            39.2          21.1           196    4150 male   2007
    ##  7 Adelie  Dream            38.8          20             190    3950 male   2007
    ##  8 Adelie  Dream            42.2          18.5           180    3550 fema…  2007
    ##  9 Adelie  Dream            37.6          19.3           181    3300 fema…  2007
    ## 10 Adelie  Dream            39.8          19.1           184    4650 male   2007
    ## # … with 114 more rows, and abbreviated variable names ¹​flipper_length_mm,
    ## #   ²​body_mass_g

``` r
#or

filter(penguins, island == "Dream")
```

    ## # A tibble: 124 × 8
    ##    species island bill_length_mm bill_depth_mm flipper_len…¹ body_…² sex    year
    ##    <fct>   <fct>           <dbl>         <dbl>         <int>   <int> <fct> <int>
    ##  1 Adelie  Dream            39.5          16.7           178    3250 fema…  2007
    ##  2 Adelie  Dream            37.2          18.1           178    3900 male   2007
    ##  3 Adelie  Dream            39.5          17.8           188    3300 fema…  2007
    ##  4 Adelie  Dream            40.9          18.9           184    3900 male   2007
    ##  5 Adelie  Dream            36.4          17             195    3325 fema…  2007
    ##  6 Adelie  Dream            39.2          21.1           196    4150 male   2007
    ##  7 Adelie  Dream            38.8          20             190    3950 male   2007
    ##  8 Adelie  Dream            42.2          18.5           180    3550 fema…  2007
    ##  9 Adelie  Dream            37.6          19.3           181    3300 fema…  2007
    ## 10 Adelie  Dream            39.8          19.1           184    4650 male   2007
    ## # … with 114 more rows, and abbreviated variable names ¹​flipper_length_mm,
    ## #   ²​body_mass_g

### 6\. Use the `distinct` function to find out what the unique species are

``` r
penguins %>%
  distinct(species)
```

    ## # A tibble: 3 × 1
    ##   species  
    ##   <fct>    
    ## 1 Adelie   
    ## 2 Gentoo   
    ## 3 Chinstrap

``` r
#or

distinct(penguins, species)
```

    ## # A tibble: 3 × 1
    ##   species  
    ##   <fct>    
    ## 1 Adelie   
    ## 2 Gentoo   
    ## 3 Chinstrap

### 7\. Use the `slice_min` function to look at the row with the smallest `bill_length_mm`

``` r
penguins %>%
  slice_min(bill_length_mm)
```

    ## # A tibble: 1 × 8
    ##   species island bill_length_mm bill_depth_mm flipper_leng…¹ body_…² sex    year
    ##   <fct>   <fct>           <dbl>         <dbl>          <int>   <int> <fct> <int>
    ## 1 Adelie  Dream            32.1          15.5            188    3050 fema…  2009
    ## # … with abbreviated variable names ¹​flipper_length_mm, ²​body_mass_g

``` r
#or

slice_min(penguins, bill_length_mm)
```

    ## # A tibble: 1 × 8
    ##   species island bill_length_mm bill_depth_mm flipper_leng…¹ body_…² sex    year
    ##   <fct>   <fct>           <dbl>         <dbl>          <int>   <int> <fct> <int>
    ## 1 Adelie  Dream            32.1          15.5            188    3050 fema…  2009
    ## # … with abbreviated variable names ¹​flipper_length_mm, ²​body_mass_g

### 8\. Use the `slice_max` function to look at the rows with the 5 largest `body_mass_g` values

``` r
penguins %>%
  slice_max(body_mass_g)
```

    ## # A tibble: 1 × 8
    ##   species island bill_length_mm bill_depth_mm flipper_leng…¹ body_…² sex    year
    ##   <fct>   <fct>           <dbl>         <dbl>          <int>   <int> <fct> <int>
    ## 1 Gentoo  Biscoe           49.2          15.2            221    6300 male   2007
    ## # … with abbreviated variable names ¹​flipper_length_mm, ²​body_mass_g

``` r
#or

slice_max(penguins, body_mass_g)
```

    ## # A tibble: 1 × 8
    ##   species island bill_length_mm bill_depth_mm flipper_leng…¹ body_…² sex    year
    ##   <fct>   <fct>           <dbl>         <dbl>          <int>   <int> <fct> <int>
    ## 1 Gentoo  Biscoe           49.2          15.2            221    6300 male   2007
    ## # … with abbreviated variable names ¹​flipper_length_mm, ²​body_mass_g

### 9\. Use the `group_by` and `slice` functions to look at the rows with the greatest `body_mass_g` for each `species`

``` r
penguins %>%
  group_by(species) %>%
  slice_max(body_mass_g)
```

    ## # A tibble: 3 × 8
    ## # Groups:   species [3]
    ##   species   island bill_length_mm bill_depth_mm flipper_le…¹ body_…² sex    year
    ##   <fct>     <fct>           <dbl>         <dbl>        <int>   <int> <fct> <int>
    ## 1 Adelie    Biscoe           43.2          19            197    4775 male   2009
    ## 2 Chinstrap Dream            52            20.7          210    4800 male   2008
    ## 3 Gentoo    Biscoe           49.2          15.2          221    6300 male   2007
    ## # … with abbreviated variable names ¹​flipper_length_mm, ²​body_mass_g
