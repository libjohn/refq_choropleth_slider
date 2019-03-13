README
================
John Little
2019-03-13

<!-- README.md is generated from README.Rmd. Please edit that file -->
The goal of refq\_choropleth\_slider was to demonstrate how to generate a plotly choropleth with a slider filtering the year. As the plot turns, I've decided that a slider filter with geom\_sf polygons is not a feasible goal. BUT, animating the choropleth via `gganimate` seems to work well.

The best **documentation for animation** will be found in the [gganimate.Rmd](gganimate.Rmd) file. Other files explore how `plotly` and/or `crosstalk` could be used to add a filter slider to the map. Those efforts proved less than idea. Lastly, I wrote a [summary report](report_slider.Rmd) which compares different visualizations, animated or note, to showing choropleths over time.

However, those efforts spawned learning more about gganimate. Summary code and output is below.

Example of `transition_time`
----------------------------

    ggplot(bg_r) +
      geom_sf(aes(fill = estimate, color = estimate)) +
      labs(title = 'Year: {round(frame_time, 0)}') +
      transition_time(as.numeric(year)) +
      shadow_mark(past = TRUE, future = TRUE)

Example of `transition_filter`
------------------------------

``` r
ggplot(bg_r) +
  geom_sf(aes(fill = estimate, color = estimate)) +
  coord_sf(datum = NA) +
  labs(title = '{next_expression}') +
  transition_filter(transition_length = 0.4, 
                    filter_length = 0.4,
                    year == "2013",
                    year == "2014",
                    year == "2015",
                    year == "2016") +
  enter_fade() +
  exit_fade() +
  shadow_mark(past = TRUE, future = TRUE)
```

![](animated_map.png "Annimated Example Choropleth")

Label Variables
---------------

Example of funking around with stringr to manipulate the label variables (see `transition_` [documentation](https://gganimate.com/reference/) for more)

``` r

yrs_txt <- c("2013", "2014", "2015", "2016")

ggplot(bg_r_small) +
  geom_sf(aes(fill = estimate, color = estimate)) +
  coord_sf(datum = NA) +
  labs(title = "YEAR: {str_replace(str_replace(as.character(next_expression), 'year == \"', ''), '\"', '')}") +
  transition_filter(transition_length = 0.4, 
                    filter_length = 0.4,
                    year == "2013",
                    year == "2014",
                    year == "2015",
                    year == "2016") +
  enter_fade() +
  exit_fade() +
  shadow_mark(past = TRUE, future = TRUE)
```

![](county_trans_filter.png "transition_filter Choropleth")
