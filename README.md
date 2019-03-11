README
================
John Little
2019-03-11

<!-- README.md is generated from README.Rmd. Please edit that file -->
The goal of refq\_choropleth\_slider was to demonstrate how to generate a plotly choropleth with a slider filtering the year. As the plot turns, I've decided that a slider filter with geom\_sf polygons is not a feasible goal. BUT, animating the choropleth via `gganimate` seems to work well.

    ggplot(bg_r) +
      geom_sf(aes(fill = estimate, color = estimate)) +
      labs(title = 'Year: {round(frame_time, 0)}') +
      transition_time(as.numeric(year)) +
      shadow_mark(past = TRUE, future = TRUE)

![](animated_map.png "Annimated Example Choropleth")
