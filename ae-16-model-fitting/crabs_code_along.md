Modeling fiddler crab size across latitudes
================

## Peek at the data

``` r
glimpse(pie_crab)
```

    ## Rows: 392
    ## Columns: 9
    ## $ date          <date> 2016-07-24, 2016-07-24, 2016-07-24, 2016-07-24, 2016-07…
    ## $ latitude      <dbl> 30, 30, 30, 30, 30, 30, 30, 30, 30, 30, 30, 30, 30, 30, …
    ## $ site          <chr> "GTM", "GTM", "GTM", "GTM", "GTM", "GTM", "GTM", "GTM", …
    ## $ size          <dbl> 12.43, 14.18, 14.52, 12.94, 12.45, 12.99, 10.32, 11.19, …
    ## $ air_temp      <dbl> 21.792, 21.792, 21.792, 21.792, 21.792, 21.792, 21.792, …
    ## $ air_temp_sd   <dbl> 6.391, 6.391, 6.391, 6.391, 6.391, 6.391, 6.391, 6.391, …
    ## $ water_temp    <dbl> 24.502, 24.502, 24.502, 24.502, 24.502, 24.502, 24.502, …
    ## $ water_temp_sd <dbl> 6.121, 6.121, 6.121, 6.121, 6.121, 6.121, 6.121, 6.121, …
    ## $ name          <chr> "Guana Tolomoto Matanzas NERR", "Guana Tolomoto Matanzas…

## Visually explore the data

Create a scatter plot that maps latitude to the x-axis and size to the
y-axis. What relationship could we test for using a statistical model?

Create a boxplot that maps name to the y-axis and size to the x-axis.
What difference could we test for using a statistical model?

## Crab size vs. latitude

Fitting the model step by step:

``` r
linear_reg() %>%                                # specify: what model will we fit?
  set_engine("lm") %>%                          # set engine : how will we fit the model?
  fit(size ~ latitude, data = pie_crab)        # fit: actually fit model based on formula
```

    ## parsnip model object
    ## 
    ## Fit time:  4ms 
    ## 
    ## Call:
    ## stats::lm(formula = size ~ latitude, data = data)
    ## 
    ## Coefficients:
    ## (Intercept)     latitude  
    ##     -3.6244       0.4851

Save the model output to an object called `crab_lat_fit`.

Now we can examine our model output.

``` r
#look at model output


#get the object names for crab_lat_fit output


#look at some of the model output objects 
```

Here, we tidy the model parameter output into a tidy dataframe. What
does the estimate value of the intercept represent? What does the
latitude estimate represent? What does the p-value represent?

We can also create tidy output for overall model statistics. What does
the R-squared represent? What does the p-value represent?

Here, we create a table containing observed values (`size`, `latitude`),
fitted values (`.fitted`) (i.e., expected or model-fitted size for each
latitude), residuals (`.resid`) (i.e., difference between
expected/fitted size and observed size for each latitude), and several
other statistics that we won’t talk about right now.

And we can use the augment table to check our residuals by plotting the
fitted values (expected values of size) vs the residuals (the difference
between the fitted size values and the actual size observations). The
points on the plot should look random - if there is any type of pattern,
then there might be another variable that is not included in the model
but has an effect on crab size.

## Crab size vs. name (sample location)

Fitting the model step by step:

\-specify: what model will we fit? -set engine : how will we fit the
model? -fit: actually fit model based on formula

Save the model output to an obmect called `crab_site_fit`.

Examine our model output.

``` r
#look at model output


#get the object names for crab_lat_fit output


#look at some of the model output objects 
```

Here, we tidy the model output into a tidy dataframe. What does the
value of the intercept represent? What do the remaining values
represent?

We can also create tidy output for model statistics.

Here, we create a table containing observed values (`size`, `latitude`),
fitted values (`.fitted`) (i.e., expected/fitted size for each site),
residuals (`.resid`) (i.e., difference between expected/fitted size and
observed size for each latitude).

And we can use it to check our residuals by plotting the fitted values
(expected values of size) vs the residuals (the difference between the
fitted size values and the actual size observations). Does our model
seem to be a good fit?
