HW2\_Markdown
================
Noah Kreski

``` r
# install.packages("devtools")
devtools::install_github("p8105/p8105.datasets")
```

    ## Skipping install of 'p8105.datasets' from a github remote, the SHA1 (21f5ad1c) has not changed since last install.
    ##   Use `force = TRUE` to force installation

``` r
library(tidyverse)
```

    ## -- Attaching packages ------------------------------------------------------------------------------------------------------------ tidyverse 1.2.1 --

    ## v ggplot2 3.0.0     v purrr   0.2.5
    ## v tibble  1.4.2     v dplyr   0.7.6
    ## v tidyr   0.8.1     v stringr 1.3.1
    ## v readr   1.1.1     v forcats 0.3.0

    ## -- Conflicts --------------------------------------------------------------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(p8105.datasets)
#Formatting appropriate names
brfss_smart2010_Tidy = janitor::clean_names(brfss_smart2010) %>%
                      #Removing unneeded variables
                      select(-class, -topic, -question, -sample_size, -(confidence_limit_low:geo_location))%>%
                      #Isolating necessary data values
                      filter(response %in% c("Excellent", "Very good", "Good", "Fair", "Poor"))%>%
                      #Splitting by response category
                      spread(key=response, value = data_value)%>%
                      janitor::clean_names()%>%
                      mutate(EVG = excellent + very_good)
```

How many unique locations are included in the dataset? Is every state represented? What state is observed the most?

In 2002, what is the median of the “Excellent” response value?

The median of the Excellent response value in 2002 is `NA`.

Make a histogram of “Excellent” response values in the year 2002.

Make a scatterplot showing the proportion of “Excellent” response values in New York County and Queens County (both in NY State) in each year from 2002 to 2010.
