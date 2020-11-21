
# cmapplot <img src="man/figures/logo.png" align="right" alt="cmapplot logo" width="128" />

<!-- badges: start -->

[![R build
status](https://github.com/CMAP-REPOS/cmapplot/workflows/R-CMD-check/badge.svg)](https://github.com/CMAP-REPOS/cmapplot/actions?query=workflow%3AR-CMD-check)
[![pkgdown build
status](https://github.com/CMAP-REPOS/cmapplot/workflows/pkgdown/badge.svg)](https://github.com/CMAP-REPOS/cmapplot/actions?query=workflow%3Apkgdown)
<!-- badges: end -->

This R package provides themes, color scales, and other custom functions
for [ggplot2](https://github.com/tidyverse/ggplot2), based on Chicago
Metropolitan Agency for Planning (CMAP) design guidelines.

## The basics

The cmapplot package contains a few key components:

1.  Apply a CMAP theme to ggplots with `theme_cmap()`
2.  Easily provide common CMAP plot customizations, such as with custom
    geoms `geom_recessions()` and `geom_text_lastonly()`
3.  Apply CMAP colors using a variety of custom functions
    (e.g. `cmap_fill_discrete()`)
4.  Place the themed plot within a CMAP layout, and export the plot from
    R if desired with `finalize_plot()`

## Installation

Run the following to install or update cmapplot:

``` r
## Install current version from GitHub
devtools::install_github("CMAP-REPOS/cmapplot", build_vignettes=TRUE)

## Then load the package as you would any other
library(cmapplot)
```

To install on macOS, users must install
[XQuartz](https://www.xquartz.org) before cmapplot can be loaded. (This
can be easily accomplished via the [Homebrew](https://brew.sh) package
manager with the command `brew cask install xquartz`.)

**A note about fonts**: The cmapplot package works best when installed
on a Windows computer with the Whitney family of fonts installed
(specifically the Book, Medium, and Semibold variants). If installed on
a Windows computer *without* Whitney, the package will still work, but
the fonts will default to Calibri. If installed on macOS or Linux, the
fonts will default to Arial, *even if Whitney is installed.*

## CMAP theme and colors

The function `theme_cmap()` returns a complete ggplot2 theme that can be
added to a ggplot code block (similar to `ggplot2::theme_minimal()` or
`ggplot2::theme_bw()`). Additionally, `theme_cmap()` accepts a variety
of arguments to additionally customize the theme output. CMAP color
functions apply colors from the CMAP color palette to the plot.

``` r
ggplot(data = pop_and_laborforce_by_age, 
       aes(x = value,
           y = interaction(year, variable, sep = " "),
           fill = age)) +
  geom_col(position = position_stack(reverse = TRUE)) +
  scale_x_continuous(labels = scales::percent) +
  theme_cmap(xlab = "Percent",
             gridlines = "v",
             vline = 0) +
  cmap_fill_discrete(palette = "environment")
#> 'Whitney' font family not found. Using a substitute...
```

<img src="man/figures/README-theme-1.png" width="672" style="display: block; margin: auto;" />

## Finalizing the plot

The function `finalize_plot()` places a ggplot within a frame defined by
CMAP design standards. It provides a variety of customization options
via arguments, and allows for in-R viewing and/or exporting in various
formats.

``` r
finalize_plot(title = "Regional population and labor force participation",
              caption = "Data from the American Community Survey",
              width = 7, height = 4.25)
```

<img src="man/figures/README-finalize-1.png" width="672" style="display: block; margin: auto;" />

## Additional reading

While this package is designed to make the application of CMAP design
standards to plots relatively easy, developing a professional, finished
plot in R will require a decent familiarity with the grammar of
[ggplot2](ggplot2.tidyverse.org/). Excellent resources in this category
already exist:

  - The [R graphics cookbook](https://r-graphics.org/) provides
    accessible examples of how to make almost [any
    type](https://r-graphics.org/recipe-miscgraph-vectorfield) of plot,
    as well as how to modify things like [limits,
    scales](https://r-graphics.org/recipe-axes-range), [coordinate
    systems](https://r-graphics.org/recipe-axes-polar), and
    [facets](https://r-graphics.org/recipe-facet-basic).

  - The [ggplot2 book](https://ggplot2-book.org/) delves deeper into why
    and how ggplot2 works the way it does, also with distinct chapters
    on topics like
    [scales](https://ggplot2-book.org/scales-guides.html), [coordinate
    systems](https://ggplot2-book.org/coord.html),
    [facets](https://ggplot2-book.org/facet.html), etc.
