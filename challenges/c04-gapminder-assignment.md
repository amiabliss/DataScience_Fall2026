Gapminder
================
Amia Georges
2026-10-01

- [Grading Rubric](#grading-rubric)
  - [Individual](#individual)
  - [Submission](#submission)
- [Guided EDA](#guided-eda)
  - [**q0** Perform your “first checks” on the dataset. What variables
    are in
    this](#q0-perform-your-first-checks-on-the-dataset-what-variables-are-in-this)
  - [**q1** Determine the most and least recent years in the `gapminder`
    dataset.](#q1-determine-the-most-and-least-recent-years-in-the-gapminder-dataset)
  - [**q2** Filter on years matching `year_min`, and make a plot of the
    GDP per capita against continent. Choose an appropriate `geom_` to
    visualize the data. What observations can you
    make?](#q2-filter-on-years-matching-year_min-and-make-a-plot-of-the-gdp-per-capita-against-continent-choose-an-appropriate-geom_-to-visualize-the-data-what-observations-can-you-make)
  - [**q3** You should have found *at least* three outliers in q2 (but
    possibly many more!). Identify those outliers (figure out which
    countries they
    are).](#q3-you-should-have-found-at-least-three-outliers-in-q2-but-possibly-many-more-identify-those-outliers-figure-out-which-countries-they-are)
  - [**q4** Create a plot similar to yours from q2 studying both
    `year_min` and `year_max`. Find a way to highlight the outliers from
    q3 on your plot *in a way that lets you identify which country is
    which*. Compare the patterns between `year_min` and
    `year_max`.](#q4-create-a-plot-similar-to-yours-from-q2-studying-both-year_min-and-year_max-find-a-way-to-highlight-the-outliers-from-q3-on-your-plot-in-a-way-that-lets-you-identify-which-country-is-which-compare-the-patterns-between-year_min-and-year_max)
- [Your Own EDA](#your-own-eda)
  - [**q5** Create *at least* three new figures below. With each figure,
    try to pose new questions about the
    data.](#q5-create-at-least-three-new-figures-below-with-each-figure-try-to-pose-new-questions-about-the-data)

*Purpose*: Learning to do EDA well takes practice! In this challenge
you’ll further practice EDA by first completing a guided exploration,
then by conducting your own investigation. This challenge will also give
you a chance to use the wide variety of visual tools we’ve been
learning.

<!-- include-rubric -->

# Grading Rubric

<!-- -------------------------------------------------- -->

Unlike exercises, **challenges will be graded**. The following rubrics
define how you will be graded, both on an individual and team basis.

## Individual

<!-- ------------------------- -->

| Category | Needs Improvement | Satisfactory |
|----|----|----|
| Effort | Some task **q**’s left unattempted | All task **q**’s attempted |
| Observed | Did not document observations, or observations incorrect | Documented correct observations based on analysis |
| Supported | Some observations not clearly supported by analysis | All observations clearly supported by analysis (table, graph, etc.) |
| Assessed | Observations include claims not supported by the data, or reflect a level of certainty not warranted by the data | Observations are appropriately qualified by the quality & relevance of the data and (in)conclusiveness of the support |
| Specified | Uses the phrase “more data are necessary” without clarification | Any statement that “more data are necessary” specifies which *specific* data are needed to answer what *specific* question |
| Code Styled | Violations of the [style guide](https://style.tidyverse.org/) hinder readability | Code sufficiently close to the [style guide](https://style.tidyverse.org/) |

## Submission

<!-- ------------------------- -->

Make sure to commit both the challenge report (`report.md` file) and
supporting files (`report_files/` folder) when you are done! Then submit
a link to Canvas. **Your Challenge submission is not complete without
all files uploaded to GitHub.**

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.2.1     ✔ readr     2.2.0
    ## ✔ forcats   1.0.1     ✔ stringr   1.6.0
    ## ✔ ggplot2   4.0.3     ✔ tibble    3.3.1
    ## ✔ lubridate 1.9.5     ✔ tidyr     1.3.2
    ## ✔ purrr     1.2.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(gapminder)
```

*Background*: [Gapminder](https://www.gapminder.org/about-gapminder/) is
an independent organization that seeks to educate people about the state
of the world. They seek to counteract the worldview constructed by a
hype-driven media cycle, and promote a “fact-based worldview” by
focusing on data. The dataset we’ll study in this challenge is from
Gapminder.

# Guided EDA

<!-- -------------------------------------------------- -->

First, we’ll go through a round of *guided EDA*. Try to pay attention to
the high-level process we’re going through—after this guided round
you’ll be responsible for doing another cycle of EDA on your own!

### **q0** Perform your “first checks” on the dataset. What variables are in this

dataset?

``` r
## TASK: Do your "first checks" here!
glimpse(gapminder)
```

    ## Rows: 1,704
    ## Columns: 6
    ## $ country   <fct> "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan", …
    ## $ continent <fct> Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, …
    ## $ year      <int> 1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, 1997, …
    ## $ lifeExp   <dbl> 28.801, 30.332, 31.997, 34.020, 36.088, 38.438, 39.854, 40.8…
    ## $ pop       <int> 8425333, 9240934, 10267083, 11537966, 13079460, 14880372, 12…
    ## $ gdpPercap <dbl> 779.4453, 820.8530, 853.1007, 836.1971, 739.9811, 786.1134, …

``` r
summary(gapminder)
```

    ##         country        continent        year         lifeExp     
    ##  Afghanistan:  12   Africa  :624   Min.   :1952   Min.   :23.60  
    ##  Albania    :  12   Americas:300   1st Qu.:1966   1st Qu.:48.20  
    ##  Algeria    :  12   Asia    :396   Median :1980   Median :60.71  
    ##  Angola     :  12   Europe  :360   Mean   :1980   Mean   :59.47  
    ##  Argentina  :  12   Oceania : 24   3rd Qu.:1993   3rd Qu.:70.85  
    ##  Australia  :  12                  Max.   :2007   Max.   :82.60  
    ##  (Other)    :1632                                                
    ##       pop              gdpPercap       
    ##  Min.   :6.001e+04   Min.   :   241.2  
    ##  1st Qu.:2.794e+06   1st Qu.:  1202.1  
    ##  Median :7.024e+06   Median :  3531.8  
    ##  Mean   :2.960e+07   Mean   :  7215.3  
    ##  3rd Qu.:1.959e+07   3rd Qu.:  9325.5  
    ##  Max.   :1.319e+09   Max.   :113523.1  
    ## 

**Observations**:

- The variables are Country, Continent, Year, lifeExp (life expectancy),
  pop (population), gdpPercap (GDP per capita)

### **q1** Determine the most and least recent years in the `gapminder` dataset.

*Hint*: Use the `pull()` function to get a vector out of a tibble.
(Rather than the `$` notation of base R.)

``` r
## TASK: Find the largest and smallest values of `year` in `gapminder`
year_max <- gapminder %>% pull(year) %>% max()
year_min <- gapminder %>% pull(year) %>% min()
```

Use the following test to check your work.

``` r
## NOTE: No need to change this
assertthat::assert_that(year_max %% 7 == 5)
```

    ## [1] TRUE

``` r
assertthat::assert_that(year_max %% 3 == 0)
```

    ## [1] TRUE

``` r
assertthat::assert_that(year_min %% 7 == 6)
```

    ## [1] TRUE

``` r
assertthat::assert_that(year_min %% 3 == 2)
```

    ## [1] TRUE

``` r
if (is_tibble(year_max)) {
  print("year_max is a tibble; try using `pull()` to get a vector")
  assertthat::assert_that(False)
}

print("Nice!")
```

    ## [1] "Nice!"

### **q2** Filter on years matching `year_min`, and make a plot of the GDP per capita against continent. Choose an appropriate `geom_` to visualize the data. What observations can you make?

You may encounter difficulties in visualizing these data; if so document
your challenges and attempt to produce the most informative visual you
can.

``` r
## TASK: Create a visual of gdpPercap vs continent
gapminder %>%
  filter(year == year_min) %>%
  ggplot(
    aes(
      x = continent,
      y = gdpPercap
      )
    ) +
  geom_boxplot() +
  scale_y_log10()
```

![](c04-gapminder-assignment_files/figure-gfm/q2-task-1.png)<!-- -->

**Observations**:

- Africa has almost a solid line for their gdp, which means it has the
  lowest gdp per capita and little variation between the gdp of the
  different countries. Oceania also has a solid line (little variation
  between countries).
- Europe has the widest distribution in its box, meaning it has the
  widest variation in gdp when comparing countries.
- Asia has an extreme outlier, which compresses the distribution for all
  the continents
- Africa, Americas, Asia, and Europe all have outliers. Oceania is the
  only one without one.

**Difficulties & Approaches**:

- It was incredibly difficult to uncompress the graph. I didn’t want to
  remove the outlier, so I looked on the internet and in the rstudio
  help page. scale_y_log10() was a fix that is contained in the ggplot
  package (?)

### **q3** You should have found *at least* three outliers in q2 (but possibly many more!). Identify those outliers (figure out which countries they are).

``` r
## TASK: Identify the outliers from q2
gapminder %>%
  filter(year == year_min) %>%
  filter(gdpPercap > 11000) %>%
  select(country, gdpPercap)
```

    ## # A tibble: 4 × 2
    ##   country       gdpPercap
    ##   <fct>             <dbl>
    ## 1 Canada           11367.
    ## 2 Kuwait          108382.
    ## 3 Switzerland      14734.
    ## 4 United States    13990.

**Observations**:

- Identify the outlier countries from q2
  - The outliers are Canada, Kuwait, Switzerland, and United States
  - I don’t think this was the best way to do this. I originally did
    \>10000, but Australia isn’t actually an outlier, Oceania just has a
    high average gdp, so I increased to \>11000

*Hint*: For the next task, it’s helpful to know a ggplot trick we’ll
learn in an upcoming exercise: You can use the `data` argument inside
any `geom_*` to modify the data that will be plotted *by that geom
only*. For instance, you can use this trick to filter a set of points to
label:

``` r
## NOTE: No need to edit, use ideas from this in q4 below
gapminder %>%
  filter(year == max(year)) %>%

  ggplot(aes(continent, lifeExp)) +
  geom_boxplot() +
  geom_point(
    data = . %>% filter(country %in% c("United Kingdom", "Japan", "Zambia")),
    mapping = aes(color = country),
    size = 2
  )
```

![](c04-gapminder-assignment_files/figure-gfm/layer-filter-1.png)<!-- -->

### **q4** Create a plot similar to yours from q2 studying both `year_min` and `year_max`. Find a way to highlight the outliers from q3 on your plot *in a way that lets you identify which country is which*. Compare the patterns between `year_min` and `year_max`.

*Hint*: We’ve learned a lot of different ways to show multiple
variables; think about using different aesthetics or facets.

``` r
## TASK: Create a visual of gdpPercap vs continent
gapminder %>%
  filter(year == year_max) %>%
  ggplot(aes(continent, gdpPercap)) +
  geom_boxplot() +
  geom_point(
    data = . %>% filter(country %in% c("Kuwait", "United States", "Switzerland", "Canada")),
    mapping = aes(color = country),
    size = 2
  )
```

![](c04-gapminder-assignment_files/figure-gfm/q4-task-1.png)<!-- -->

``` r
  gapminder %>%
    filter(year == year_min) %>%
             ggplot(aes(continent, gdpPercap)) +
             geom_boxplot() +
             geom_point(
               data = . %>% filter(country %in% c("Kuwait", "United States", "Switzerland", "Canada")),
               mapping = aes(color = country),
               size = 2
             )
```

![](c04-gapminder-assignment_files/figure-gfm/q4-task-2.png)<!-- -->

**Observations**:

- In the second graph, year_min, Kuwait is an extreme outlier with over
  90000 gdp per capita, condensing the overall graph. In the first
  (year_max) graph, Kuwait has decreased to under 50000. It is still a
  outlier but a much smaller scale.
- Canada and the US become much larger outliers in the year_max graph.
- Switzerland seems to have become a slightly smaller outlier when
  compared to the rest of Europe

# Your Own EDA

<!-- -------------------------------------------------- -->

Now it’s your turn! We just went through guided EDA considering the GDP
per capita at two time points. You can continue looking at outliers,
consider different years, repeat the exercise with `lifeExp`, consider
the relationship between variables, or something else entirely.

### **q5** Create *at least* three new figures below. With each figure, try to pose new questions about the data.

``` r
## TASK: Your first graph
gapminder %>%
  filter(year == year_min) %>%
  ggplot(
    aes(
      x = continent,
      y = pop
    )
  ) +
  geom_boxplot() +
  scale_y_log10()
```

![](c04-gapminder-assignment_files/figure-gfm/q5-task1-1.png)<!-- -->

``` r
gapminder %>%
  filter(year == year_min, continent == "Europe", pop < 1e6) %>%
  select(country, pop)
```

    ## # A tibble: 2 × 2
    ##   country       pop
    ##   <fct>       <int>
    ## 1 Iceland    147962
    ## 2 Montenegro 413834

``` r
gapminder %>%
  filter(year == year_min, continent == "Americas", pop > 1e8) %>%
  select(country, pop)
```

    ## # A tibble: 1 × 2
    ##   country             pop
    ##   <fct>             <int>
    ## 1 United States 157553000

- I wanted to see how population sizes varied across continents (1952).
- The Americas have a high population outlier (United States), while
  Europe has two low population outliers (Iceland, Montenegro).
- Asia has the widest range of population size, with whiskers stretching
  the furthest.
- Asia has the highest median population, while Africa has the lowest.
- Oceania has a very narrow distribution

``` r
## TASK: Your second graph
gapminder %>%
  filter(year == year_max) %>%
  ggplot(aes(x = pop, y = lifeExp, color = continent)) +
  geom_point() +
  scale_x_log10()
```

![](c04-gapminder-assignment_files/figure-gfm/q5-task2-1.png)<!-- -->

``` r
gapminder %>%
  filter(year == year_max, continent == "Asia", lifeExp < 45) %>%
  select(country, pop)
```

    ## # A tibble: 1 × 2
    ##   country          pop
    ##   <fct>          <int>
    ## 1 Afghanistan 31889923

- I wanted to see if there were any trends between population and life
  expectancy, but it doesn’t seem like there are any.
- Oceania and Europe cluster around the top, with overall high life
  expectancy across a variety of population sizes.
- Africa clusters towards the bottom of the plot, with low average life
  expectancies.
- There seems to be one country in Asia with a very low life expectancy
  compared to the rest of Asia (Afghanistan).

``` r
## TASK: Your third graph
gapminder %>%
  filter(year == year_max) %>%
  ggplot(aes(x = pop, y = gdpPercap, color = continent))+
  geom_point()+
  scale_x_log10()
```

![](c04-gapminder-assignment_files/figure-gfm/q5-task3-1.png)<!-- -->

- I wanted to see if there was a trend in the population vs gdp per
  capita, but I don’t see any large trends.
- Europe seems to generally have higher gdp per capita despite large
  changes in population. Africa has the same trend, but with a lower gdp
  across a wide variety of populations.
