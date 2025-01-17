
## Michelle Qin's additions for Biostat 777 class

For my Biostat 777 class (taken fall 2023), I was thrilled to create a [website](https://jhu-statprogramming-fall-2023.github.io/biostat777-project3-part1-m-qin/) for the R package `CombineDistributions`. I first used `CombineDistributions` two and a half years ago when I worked with Dr. Emily Howerton (the creator of this package), Dr. Cecile Viboud, and other scientists at the [COVID-19 Scenario Modeling Hub](https://covid19scenariomodelinghub.org). Our task was to project U.S. COVID-19 cases, hospitalizations, and deaths from one week to six months ahead. Such long-term infectious disease modeling required us to carefully combine multiple expert modeling teams' projections and quantify their combined uncertainty, motivating Dr. Howerton et al.'s methodological work in this area.

### The `pkgdown` website

Using `pkgdown`, I created a website to help users use the `CombineDistributions` package. I made some customizations in my website:

1. I set the theme of the website to be "yeti", a Bootswatch theme.
2. I reordered the vignettes in the navbar to start from the introduction rather than following an alphabetical order, which was the default.
3. In the sidebar of the homepage and in the footer of the website, I credited Dr. Howerton as the author and creator of the package.
4. I updated the sidebar of the homepage to reflect the license that Dr. Howerton's original package uses [CC-BY-NC](http://creativecommons.org/licenses/by-nc/3.0/).
5. In the DESCRIPTION file, I wrote a title for the website: "Combine probabilistic predictions by averaging probabilities or quantiles".
6. I updated the README of the package, which is printed on the homepage of the website as well, to include the [paper](http://doi.org/10.1098/rsif.2022.0659) that Dr. Howerton et al. published after the package was published on [Zenodo](https://doi.org/10.5281/zenodo.7437280).
7. I had some errors when running `devtools::check()`, so I edited some of the package's scripts and files. I may not have caught everything though.

### Exported functions in this package

`CombineDistributions` exports the following functions:

- `LOP()`: "Given a set of cumulative distribution functions (assume for now: defined on same values), combine using probability averaging (also called linear opinion pool). This method calculates the (weighted) average of quantiles at a given value."
- `aggregate_cdfs()`, which is defined in the *implementAggregation.R* file: "Given a data.frame containing cdfs, return a single aggregate cdf using specified method."
- `vincent()`: "Given a set of cumulative distribution functions  (assume for now: defined on same values), combine using quantile averaging (also called Vincent average). This method calculates the (weighted) average of values at a given quantile."


A basic example for the function `LOP()`, taken from its documentation:  

    dat <- expand.grid(id = c("A", "B"),
                       quantile = seq(0,1,0.01))
    dat$value <- ifelse(dat$id == "A", qnorm(dat$quantile), qnorm(dat$quantile, 0,2))
    LOP(dat$quantile, dat$value, dat$id, seq(0,1,0.05), NA)

## Miscellaneous comment(s)

The original package exports a `data/` folder, containing files that are generated by R scripts in the `data-raw/` folder, exported by a script called `data.R` in the `R` folder, and used in a vignette. Following my TA's advice about R packages, I have deleted the `data/` folder and `R/data.R` from my forked repository.


# CombineDistributions

This package implements multiple methods for combining probabilistic predictions, including probability and quantile averaging, i.e.,   Linear Opinion Pool (Stone 1961) and Vincent average (Vincent 1912, Ratcliff 1979) respectively, as well as non-equal weighting, including trimming methods (Jose 2014). 


All code is licensed under the CC-BY-NC [(Creative Commons attribution-noncommercial)](http://creativecommons.org/licenses/by-nc/3.0/) license. This package can be referenced by citing 

<center> Emily Howerton, Lucie Contamin, & SungmokJung. (2022). eahowerton/CombineDistributions: v0.2 release (v0.2.0). Zenodo. https://doi.org/10.5281/zenodo.7437280 </center>  


and is available on GitHub at [https://github.com/eahowerton/CombineDistributions](https://github.com/eahowerton/CombineDistributions).


## Installation

You can install the released version of CombineDistributions from GitHub with:

    remotes::install_github("eahowerton/CombineDistributions")


## Vignettes
Please reference our vignettes to see examples of the functionality in `CombineDistributions`. 

1. Introduction to `CombineDistributions`: this vignette provides an overview of the aggregation methods available and how to implement them.

2. Aggregating predictions from an SIRS mdoel: this vignette illustrates a simple simulation case study, where we simulate a multi-model prediction effort and compare aggregation methods in this controlled environment. 

3. Aggregation and trimming on real-world COVID-19 death predictions: this vignette aggregates projections on COVID-19 deaths from 17 distinct epidemiological models, including varying the aggregation approach and the weighting scheme.

## References

Howerton, Emily, Runge, Michael C., Bogich, Tiffany L., Borchering, Rebecca K., Inamine, Hidetoshi, Lessler, Justin, Mullany, Luke C., Probert, William J. M., Smith, Claire P., Truelove, Shaun, Viboud, Cécile, and Shea, Katriona. 2023. "Context-dependent representation of within- and between-model uncertainty: aggregating probabilistic predictions in infectious disease epidemiology." J. R. Soc. Interface 20:20220659. http://doi.org/10.1098/rsif.2022.0659.

Jose, Victor Richmond R., Yael Grushka-Cockayne, and Kenneth C. Lichtendahl. 2014. “Trimmed Opinion Pools and the Crowd’s Calibration Problem.” Management Science 60 (2): 463–75. https://doi.org/10.1287/mnsc.2013.1781.

Ratcliff, Roger. 1979. “Group Reaction Time Distributions and an Analysis of Distribution Statistics.” Psychological Bulletin 86 (3): 446–61. https://doi.org/10.1037/0033-2909.86.3.446.

Stone, M. 1961. “The Opinion Pool.” The Annals of Mathematical Statistics 32 (4): 1339–42.

Vincent, Stella Burnham. 1912. “The Function of the Vibrissae in the Behavior of the White Rat.” Cambridge MA: Holt.

