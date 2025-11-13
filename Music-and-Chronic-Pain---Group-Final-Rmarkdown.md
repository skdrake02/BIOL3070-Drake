Music and Chronic Pain - Rmarkdown Final
================
Sydney Drake
2025-11-13

- [ABSTRACT](#abstract)
- [QUESTION](#question)
- [HYPOTHESIS](#hypothesis)
- [PREDICTION](#prediction)
- [STATISTICAL TEST](#statistical-test)
- [VISUALIZATION - BAR PLOT GRAPH](#visualization---bar-plot-graph)
- [REFERENCES](#references)

# ABSTRACT

\#INTRODUCTION

Fibromyalgia is a disease characterized by chronic, widespread pain and
fatigue. Such a condition negatively impacts an individual’s ability to
function in daily life. As there is no easy treatment to improve these
individual’s quality of life, it is of the utmost importance to study a
wide variety of therapies and treatments to improve how this condition
is addressed.

Classical music, for example, has long been associated with benefits in
treatment and outcome.

Our study addresses the affect of music on an individual’s experience of
chronic pain due to fibromyalgia. Participants in this study, all with
this condition, split into two groups: control and treatment. These two
groups are questioned about their pain level before then receiving the
music treatment, either the control or music. The pain level of the
participants is then once again taken.

This study is important because it addresses a significant need in our
society. Many individuals who struggle with this chronic pain have had
unsatisfactory results with traditional medicine and treatment. Relief
from chronic pain would improve quality of life for millions of
Americans, thereby improving society and furthering our understanding of
this disease.

# QUESTION

Does music treatment decrease the experience of chronic pain associated
with fibromyalgia?

# HYPOTHESIS

Participants with fibromyalgia experiencing chronic pain will report
less pain while listening to music compared to pink noise (control).
Additionally, participants will report lower pain after listening to
music than before music treatment.

# PREDICTION

We predict to see lower rates of pain in individuals after receiving
music treatment compared to individuals who received the control
treatment. We expect to see correlated significance in our statistical
tests.

# STATISTICAL TEST

We will test the significance of our data using Repeated-Measures ANOVA,
which will compare pain level across each of the individual’s four
conditions: initial pain, pain after pink noise, as well as pain before
and after music of choice.

For visualization, we will compare the bar plot of individual’s pain
scores across these three conditions.

# VISUALIZATION - BAR PLOT GRAPH

In the x-axis of the bar plot are 4 conditions. pic1 is the first
control, which measures pain level before playing pink music, and pic2
measures pain level after the pink music. pim1 and pim2 show pain levels
before and after playing music of choice respectively.

``` r
library(ggplot2)
library(tidyr)
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
data <- read.csv("dataset.csv")

data_long <- data %>%
  pivot_longer(
    cols = c(pic1, pic2, pim1, pim2),
    names_to = "treatment",
    values_to = "value"
  )

ggplot(
  data_long %>%
    mutate(
      treatment = recode(
        treatment,
        pic1 = "Before Control",
        pic2 = "After Control",
        pim1 = "Before Music",
        pim2 = "After Music"
      ),
      treatment = factor(
        treatment,
        levels = c("Before Control", "After Control", "Before Music", "After Music")
      )
    ),
  aes(x = treatment, y = value, fill = treatment)
) +
  geom_boxplot(alpha = 0.6) +
  scale_y_continuous(breaks = seq(0, 10, 1)) +
  coord_cartesian(ylim = c(0, 10)) +
  scale_fill_brewer(palette = "Spectral") +
  theme_classic() +
  theme(
    legend.position = "none",
    axis.text.x = element_text(size = 12, face = "bold"),
    axis.text.y = element_text(size = 12),
    axis.title.x = element_text(size = 16, face = "bold", margin = margin(t = 10)),
    axis.title.y = element_text(size = 16, face = "bold", margin = margin(r = 10))
  ) +
  xlab("Pain Intensity") +
  ylab("Pain Level")
```

    ## Warning: Removed 92 rows containing non-finite outside the scale range
    ## (`stat_boxplot()`).

![](Music-and-Chronic-Pain---Group-Final-Rmarkdown_files/figure-gfm/code%20chunk%201-1.png)<!-- -->

``` r
# Pivot pic1 and pic2 into long format
data_long <- data %>%
  pivot_longer(cols = c(pic1, pic2), names_to = "treatment", values_to = "value")

# Make boxplot
ggplot(data_long, aes(x = treatment, y = value, fill = treatment)) +
  geom_boxplot(alpha = 0.7, width = 0.6) +
  theme_classic() +
  scale_fill_brewer(palette = "Set1") +
  ylab("Pain Level") +
  xlab("Pain Intensity-Control 1 (before) and Pain Intensity-Control 2 (after)") +
  theme(
    axis.text = element_text(size = 14),
    axis.title = element_text(size = 12, face = "bold"),
    legend.position = "none"
  )
```

    ## Warning: Removed 46 rows containing non-finite outside the scale range
    ## (`stat_boxplot()`).

![](Music-and-Chronic-Pain---Group-Final-Rmarkdown_files/figure-gfm/code%20chunk%202-1.png)<!-- -->

``` r
library(ggplot2)
library(tidyr)
library(dplyr)

# Read your dataset
data <- read.csv("dataset.csv")

# Pivot pic2 and pim2 into long format
data_long <- data %>%
  pivot_longer(cols = c(pim1, pim2), names_to = "treatment", values_to = "value")

# Make boxplot
ggplot(data_long, aes(x = treatment, y = value, fill = treatment)) +
  geom_boxplot(alpha = 0.7, width = 0.6) +
  theme_classic() +
  scale_fill_brewer(palette = "Set1") +
  ylab("Pain Level") +
  xlab("Pain Intensity-Music 1 (before) and Pain Intensity-Music 2 (after)") +
  theme(
    axis.text = element_text(size = 14),
    axis.title = element_text(size = 12, face = "bold"),
    legend.position = "none"
  )
```

    ## Warning: Removed 46 rows containing non-finite outside the scale range
    ## (`stat_boxplot()`).

![](Music-and-Chronic-Pain---Group-Final-Rmarkdown_files/figure-gfm/3rd%20code%20chunk-1.png)<!-- -->

``` r
library(ggplot2)
library(tidyr)
library(dplyr)

data <- read.csv("dataset.csv")

# Pivot pim1 and pim2 into long format
data_long_pim <- data %>%
  pivot_longer(cols = c(pic2, pim2), names_to = "treatment", values_to = "value")

# Make boxplot
ggplot(data_long_pim, aes(x = treatment, y = value, fill = treatment)) +
  geom_boxplot(alpha = 0.7, width = 0.6) +
  theme_classic() +
  scale_fill_brewer(palette = "Set1") +
  ylab("Pain Level") +
  xlab("Pain Intensity-Control 2 (after) and Pain Intensity-Music 2 (after)") +
  theme(
    axis.text = element_text(size = 14),
    axis.title = element_text(size = 12, face = "bold"),
    legend.position = "none"
  )
```

    ## Warning: Removed 46 rows containing non-finite outside the scale range
    ## (`stat_boxplot()`).

![](Music-and-Chronic-Pain---Group-Final-Rmarkdown_files/figure-gfm/code%20chunk%20pic2%20vs%20pim2-1.png)<!-- -->

# REFERENCES

1.  ChatGPT. OpenAI, version Jan 2025. Used as a reference for functions
    such as plot() and to correct syntax errors. Accessed 2025-11-13.
2.  R-graph gallery. Used as a template for bar plot graph coding.
    Accessed 10/30/2025.
