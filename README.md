
-   [Infer: a grammar for statistical inference](#infer-a-grammar-for-statistical-inference)
    -   [Hypothesis tests](#hypothesis-tests)
    -   [Confidence intervals](#confidence-intervals)

Infer: a grammar for statistical inference
------------------------------------------

The objective of this package is to perform statistical inference using a grammar that illustrates the underlying concepts and a format that coheres with the `tidyverse`. To participate in the discussion surrounding the development of this package, please see the issues.

### Hypothesis tests

![h-test diagram](figs/ht-diagram.png)

#### Examples

One categorical (2 level) variable

    mtcars %>%
    select(am) %>%
    hypothesis(null = “p = 25”) %>% # would require string parsing
    generate(repeat = 100) %>% # here it’d be doing simulation
    calculate(stat = “prop”) #

Two categorical (2 level) variables

    mtcars %>%
    select(am, vs) %>%
    hypothesis(null = “independence”) %>% # 
    generate(repeat = 100) %>%
    calculate(stat = “diff in prop”) #

One categorical (&gt;2 level) - GoF

    mtcars %>%
    select(cyl) %>%
    hypothesis(null = “p1 = .33, p2 = .33, p3 = .33”) %>%
    generate(repeat = 100) %>%
    calculate(stat = “chisq”)

Two categorical (&gt;2 level) variables

    mtcars %>%
    select(cyl, am) %>%
    hypothesis(null = “independence”) %>%
    generate(repeat = 100) %>%
    calculate(stat = “chisq”)

One numerical variable one categorical (2 levels) (diff in means)

    mtcars %>%
    select(mpg, am) %>%
    hypothesis(null = “equal means”) %>%
    generate(repeat = 100) %>%
    calculate(stat = “diff in means”)

One numerical one categorical (&gt;2 levels) - ANOVA

    mtcars %>%
    select(mpg, cyl) %>%
    hypothesis(null = “equal means”) %>%
    generate(repeat = 100) %>%
    calculate(stat = “F”)

Two numerical vars - SLR

    mtcars %>%
    select(mpg, hp) %>%
    hypothesis(null = “independence”) %>% # or “slope = 0”
    generate(repeat = 100) %>%
    calculate(stat = “lm(mpg ~ hp)”)

### Confidence intervals
