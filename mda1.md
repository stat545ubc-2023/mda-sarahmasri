Mini Data-Analysis Deliverable 1
================

# Welcome to your (maybe) first-ever data analysis project!

And hopefully the first of many. Let’s get started:

1.  Install the [`datateachr`](https://github.com/UBC-MDS/datateachr)
    package by typing the following into your **R terminal**:

<!-- -->

    install.packages("devtools")
    devtools::install_github("UBC-MDS/datateachr")

2.  Load the packages below.

``` r
library(datateachr)
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.3     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

3.  Make a repository in the <https://github.com/stat545ubc-2023>
    Organization. You can do this by following the steps found on canvas
    in the entry called [MDA: Create a
    repository](https://canvas.ubc.ca/courses/126199/pages/mda-create-a-repository).
    One completed, your repository should automatically be listed as
    part of the stat545ubc-2023 Organization.

# Instructions

## For Both Milestones

- Each milestone has explicit tasks. Tasks that are more challenging
  will often be allocated more points.

- Each milestone will be also graded for reproducibility, cleanliness,
  and coherence of the overall Github submission.

- While the two milestones will be submitted as independent
  deliverables, the analysis itself is a continuum - think of it as two
  chapters to a story. Each chapter, or in this case, portion of your
  analysis, should be easily followed through by someone unfamiliar with
  the content.
  [Here](https://swcarpentry.github.io/r-novice-inflammation/06-best-practices-R/)
  is a good resource for what constitutes “good code”. Learning good
  coding practices early in your career will save you hassle later on!

- The milestones will be equally weighted.

## For Milestone 1

**To complete this milestone**, edit [this very `.Rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-1.Rmd)
directly. Fill in the sections that are tagged with
`<!--- start your work below --->`.

**To submit this milestone**, make sure to knit this `.Rmd` file to an
`.md` file by changing the YAML output settings from
`output: html_document` to `output: github_document`. Commit and push
all of your work to the mini-analysis GitHub repository you made
earlier, and tag a release on GitHub. Then, submit a link to your tagged
release on canvas.

**Points**: This milestone is worth 36 points: 30 for your analysis, and
6 for overall reproducibility, cleanliness, and coherence of the Github
submission.

# Learning Objectives

By the end of this milestone, you should:

- Become familiar with your dataset of choosing
- Select 4 questions that you would like to answer with your data
- Generate a reproducible and clear report using R Markdown
- Become familiar with manipulating and summarizing your data in tibbles
  using `dplyr`, with a research question in mind.

# Task 1: Choose your favorite dataset

The `datateachr` package by Hayley Boyce and Jordan Bourak currently
composed of 7 semi-tidy datasets for educational purposes. Here is a
brief description of each dataset:

- *apt_buildings*: Acquired courtesy of The City of Toronto’s Open Data
  Portal. It currently has 3455 rows and 37 columns.

- *building_permits*: Acquired courtesy of The City of Vancouver’s Open
  Data Portal. It currently has 20680 rows and 14 columns.

- *cancer_sample*: Acquired courtesy of UCI Machine Learning Repository.
  It currently has 569 rows and 32 columns.

- *flow_sample*: Acquired courtesy of The Government of Canada’s
  Historical Hydrometric Database. It currently has 218 rows and 7
  columns.

- *parking_meters*: Acquired courtesy of The City of Vancouver’s Open
  Data Portal. It currently has 10032 rows and 22 columns.

- *steam_games*: Acquired courtesy of Kaggle. It currently has 40833
  rows and 21 columns.

- *vancouver_trees*: Acquired courtesy of The City of Vancouver’s Open
  Data Portal. It currently has 146611 rows and 20 columns.

**Things to keep in mind**

- We hope that this project will serve as practice for carrying our your
  own *independent* data analysis. Remember to comment your code, be
  explicit about what you are doing, and write notes in this markdown
  document when you feel that context is required. As you advance in the
  project, prompts and hints to do this will be diminished - it’ll be up
  to you!

- Before choosing a dataset, you should always keep in mind **your
  goal**, or in other ways, *what you wish to achieve with this data*.
  This mini data-analysis project focuses on *data wrangling*,
  *tidying*, and *visualization*. In short, it’s a way for you to get
  your feet wet with exploring data on your own.

And that is exactly the first thing that you will do!

1.1 **(1 point)** Out of the 7 datasets available in the `datateachr`
package, choose **4** that appeal to you based on their description.
Write your choices below:

**Note**: We encourage you to use the ones in the `datateachr` package,
but if you have a dataset that you’d really like to use, you can include
it here. But, please check with a member of the teaching team to see
whether the dataset is of appropriate complexity. Also, include a
**brief** description of the dataset here to help the teaching team
understand your data.

<!-------------------------- Start your work below ---------------------------->

1.  **cancer_sample**: *Data includes 569 tumours, their diagnosis
    (malignant or benign) and physical attributes of each tumour.*
2.  **vancouver_trees**: *Listing of 146611 publics trees on Vancouver
    streets.*
3.  **apt_buildings**: *Listing of 3455 Toronto apartments and their
    attributes.*
4.  **steam_games**: *Includes 40833 games available on Steam shop and
    their descriptions/attributes.*

<!----------------------------------------------------------------------------->

1.2 **(6 points)** One way to narrowing down your selection is to
*explore* the datasets. Use your knowledge of dplyr to find out at least
*3* attributes about each of these datasets (an attribute is something
such as number of rows, variables, class type…). The goal here is to
have an idea of *what the data looks like*.

*Hint:* This is one of those times when you should think about the
cleanliness of your analysis. I added a single code chunk for you below,
but do you want to use more than one? Would you like to write more
comments outside of the code chunk?

<!-------------------------- Start your work below ---------------------------->

The following three attributes were found over the selected four
datasets: - number of rows - number of columns - proportion of missing
values

***cancer_sample***: From the UCI Machine Learning Repository. There are
569 rows, 32 columns, and no missing values.

``` r
cancer_sample %>% summarize(nrow = n(), ncol = ncol(.), prop_na = sum(is.na(.))/(n() * ncol(.)))
```

    ## # A tibble: 1 × 3
    ##    nrow  ncol prop_na
    ##   <int> <int>   <dbl>
    ## 1   569    32       0

***vancouver_trees***: From The City of Vancouver’s Open Data Portal.
There are 146611 rows, 20 columns, and approximately 6.5% of values
missing from the dataset.

``` r
vancouver_trees %>% summarize(nrow = n(), ncol = ncol(.), prop_na = sum(is.na(.))/(n() * ncol(.)))
```

    ## # A tibble: 1 × 3
    ##     nrow  ncol prop_na
    ##    <int> <int>   <dbl>
    ## 1 146611    20  0.0652

***apt_buildings***: From The City of Toronto’s Open Data Portal. There
are 3455 rows, 37 columns, and approximately 4.9% of values missing from
the dataset.

``` r
apt_buildings %>% summarize(nrow = n(), ncol = ncol(.), prop_na = sum(is.na(.))/(n() * ncol(.)))
```

    ## # A tibble: 1 × 3
    ##    nrow  ncol prop_na
    ##   <int> <int>   <dbl>
    ## 1  3455    37  0.0492

***building_permits***: From The City of Vancouver’s Open Data Portal.
There are 20680 rows, 14 columns, and approximately 21.1% of values
missing from the dataset.

``` r
steam_games %>% summarize(nrow = n(), ncol = ncol(.), prop_na = sum(is.na(.))/(n() * ncol(.)))
```

    ## # A tibble: 1 × 3
    ##    nrow  ncol prop_na
    ##   <int> <int>   <dbl>
    ## 1 40833    21   0.211

<!----------------------------------------------------------------------------->

1.3 **(1 point)** Now that you’ve explored the 4 datasets that you were
initially most interested in, let’s narrow it down to 1. What lead you
to choose this one? Briefly explain your choice below.

<!-------------------------- Start your work below ---------------------------->

The selected dataset for this mini data analysis is the
***cancer_sample*** dataset. From the four datasets of interest explored
in the above, this is the only dataset with no missing values. It will
not be necessary to remove any rows or columns to account for null
values.

<!----------------------------------------------------------------------------->

1.4 **(2 points)** Time for a final decision! Going back to the
beginning, it’s important to have an *end goal* in mind. For example, if
I had chosen the `titanic` dataset for my project, I might’ve wanted to
explore the relationship between survival and other variables. Try to
think of 1 research question that you would want to answer with your
dataset. Note it down below.

<!-------------------------- Start your work below ---------------------------->

I would like to explore the relationship between attributes of a tumor
and it’s classification (malignant or benign). A particular research
question of interest is: “Can a tumor’s classification be predicted
using it’s prognostic factors (texture, size, shape, etc.)?”

<!----------------------------------------------------------------------------->

# Important note

Read Tasks 2 and 3 *fully* before starting to complete either of them.
Probably also a good point to grab a coffee to get ready for the fun
part!

This project is semi-guided, but meant to be *independent*. For this
reason, you will complete tasks 2 and 3 below (under the **START HERE**
mark) as if you were writing your own exploratory data analysis report,
and this guidance never existed! Feel free to add a brief introduction
section to your project, format the document with markdown syntax as you
deem appropriate, and structure the analysis as you deem appropriate. If
you feel lost, you can find a sample data analysis
[here](https://www.kaggle.com/headsortails/tidy-titarnic) to have a
better idea. However, bear in mind that it is **just an example** and
you will not be required to have that level of complexity in your
project.

# Task 2: Exploring your dataset

If we rewind and go back to the learning objectives, you’ll see that by
the end of this deliverable, you should have formulated *4* research
questions about your data that you may want to answer during your
project. However, it may be handy to do some more exploration on your
dataset of choice before creating these questions - by looking at the
data, you may get more ideas. **Before you start this task, read all
instructions carefully until you reach START HERE under Task 3**.

2.1 **(12 points)** Complete *4 out of the following 8 exercises* to
dive deeper into your data. All datasets are different and therefore,
not all of these tasks may make sense for your data - which is why you
should only answer *4*.

Make sure that you’re using dplyr and ggplot2 rather than base R for
this task. Outside of this project, you may find that you prefer using
base R functions for certain tasks, and that’s just fine! But part of
this project is for you to practice the tools we learned in class, which
is dplyr and ggplot2.

1.  Plot the distribution of a numeric variable.
2.  Create a new variable based on other variables in your data (only if
    it makes sense)
3.  Investigate how many missing values there are per variable. Can you
    find a way to plot this?
4.  Explore the relationship between 2 variables in a plot.
5.  Filter observations in your data according to your own criteria.
    Think of what you’d like to explore - again, if this was the
    `titanic` dataset, I may want to narrow my search down to passengers
    born in a particular year…
6.  Use a boxplot to look at the frequency of different observations
    within a single variable. You can do this for more than one variable
    if you wish!
7.  Make a new tibble with a subset of your data, with variables and
    observations that you are interested in exploring.
8.  Use a density plot to explore any of your variables (that are
    suitable for this type of plot).

2.2 **(4 points)** For each of the 4 exercises that you complete,
provide a *brief explanation* of why you chose that exercise in relation
to your data (in other words, why does it make sense to do that?), and
sufficient comments for a reader to understand your reasoning and code.

<!-------------------------- Start your work below ---------------------------->

#### 1. Plot the distribution of a numeric variable.

I chose this excercise from my suspicion that the distribution of
numeric variables describing a tumour will be non-uniform. This will
give me a sense of the most common values for a variable, and if values
far from the mean follow a pattern with respect to the diagnosis.

The values have been coloured by diagnosis. It seems malignant tumours
tend to have a greater area mean than that of benign tumours in the
dataset.

``` r
cancer_sample %>%  ggplot(aes(area_mean, colour = diagnosis)) + geom_histogram() + ggtitle("Radius Mean Distribution")
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](mda1_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

#### 4. Explore the relationship between 2 variables in a plot.

I chose this exercise to explore variables I am unfamiliar with. It
seems extremely likely that variables such as radius mean and perimeter
mean will have a strong, positive, linear relationship (perimeter =
$2\pi\ \times$ radius$^2$). However, I chose this exercise to better
understand other variables, such as concavity, and explore if they are
related to others. This is important to know since high correlation of
variables may result in colinearity, if applicable to milestone two.

``` r
cancer_sample %>%  ggplot(aes(radius_mean, perimeter_mean)) + geom_point() + theme_minimal() + facet_wrap(~ diagnosis) + ggtitle("Perimeter Means vs. Radius Mean per Diagnosis")
```

![](mda1_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
cancer_sample %>%  ggplot(aes(radius_mean, area_mean)) + geom_point() + theme_minimal() + facet_wrap(~ diagnosis) + ggtitle("Area Mean vs. Radius Mean per Diagnosis")
```

![](mda1_files/figure-gfm/unnamed-chunk-7-2.png)<!-- -->

``` r
cancer_sample %>%  ggplot(aes(area_mean, concavity_mean)) + geom_point() + theme_minimal() + facet_wrap(~ diagnosis) + ggtitle("Concavity Mean vs. Area Mean per Diagnosis")
```

![](mda1_files/figure-gfm/unnamed-chunk-7-3.png)<!-- -->

``` r
cancer_sample %>%  ggplot(aes(concave_points_mean, concavity_mean)) + geom_point() + theme_minimal() + facet_wrap(~ diagnosis) + ggtitle("Concavity Mean vs. Concavity Points Mean per Diagnosis")
```

![](mda1_files/figure-gfm/unnamed-chunk-7-4.png)<!-- -->

#### 7. Make a new tibble with a subset of your data, with variables and observations that you are interested in exploring.

Since many variables in this dataset are likely to be correlated, it
would be wise to reduce the variables captured to avoid a multilinearity
problem. This exercise will allow me to focus on a subset of variables
that I am particularly interested in exploring.

I choose to explore only the mean values in the data set (each attribute
includes its mean, standard error, and worst value). Additionally, I
will remove perimeter_mean and area_mean since they are highly
correlated with radius_mean. I will also remove concavity_points_mean
since it seems from the pervious exercise it might be related to
concavity_mean.

``` r
cancer_sample_reduced <- cancer_sample %>%  select(diagnosis, radius_mean, texture_mean, smoothness_mean, 
                                                   compactness_mean, concavity_mean, symmetry_mean, fractal_dimension_mean)
cancer_sample_reduced
```

    ## # A tibble: 569 × 8
    ##    diagnosis radius_mean texture_mean smoothness_mean compactness_mean
    ##    <chr>           <dbl>        <dbl>           <dbl>            <dbl>
    ##  1 M                18.0         10.4          0.118            0.278 
    ##  2 M                20.6         17.8          0.0847           0.0786
    ##  3 M                19.7         21.2          0.110            0.160 
    ##  4 M                11.4         20.4          0.142            0.284 
    ##  5 M                20.3         14.3          0.100            0.133 
    ##  6 M                12.4         15.7          0.128            0.17  
    ##  7 M                18.2         20.0          0.0946           0.109 
    ##  8 M                13.7         20.8          0.119            0.164 
    ##  9 M                13           21.8          0.127            0.193 
    ## 10 M                12.5         24.0          0.119            0.240 
    ## # ℹ 559 more rows
    ## # ℹ 3 more variables: concavity_mean <dbl>, symmetry_mean <dbl>,
    ## #   fractal_dimension_mean <dbl>

#### 8. Use a density plot to explore any of your variables (that are suitable for this type of plot).

Similarly to the first exercise, I am particularly interested in
observing the different characteristics of tumours with respect to the
diagnosis. In other words, I chose this exercise to see if distributions
for each attribute vary for malignant versus benign tumours. I observe
distributions for each variable selected in the previous exercise.

``` r
cancer_sample %>% ggplot(aes(radius_mean, diagnosis)) + ggridges::geom_density_ridges() + ggtitle("Radius Mean Density")
```

    ## Picking joint bandwidth of 0.731

![](mda1_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

``` r
cancer_sample %>% ggplot(aes(texture_mean, diagnosis)) + ggridges::geom_density_ridges() + ggtitle("Texture Mean Density")
```

    ## Picking joint bandwidth of 0.988

![](mda1_files/figure-gfm/unnamed-chunk-9-2.png)<!-- -->

``` r
cancer_sample %>% ggplot(aes(smoothness_mean, diagnosis)) + ggridges::geom_density_ridges() + ggtitle("Smoothness Mean Density")
```

    ## Picking joint bandwidth of 0.00377

![](mda1_files/figure-gfm/unnamed-chunk-9-3.png)<!-- -->

``` r
cancer_sample %>% ggplot(aes(compactness_mean, diagnosis)) + ggridges::geom_density_ridges() + ggtitle("Compactness Mean Density")
```

    ## Picking joint bandwidth of 0.0116

![](mda1_files/figure-gfm/unnamed-chunk-9-4.png)<!-- -->

``` r
cancer_sample %>% ggplot(aes(concavity_mean, diagnosis)) + ggridges::geom_density_ridges() + ggtitle("Concavity Mean Density")
```

    ## Picking joint bandwidth of 0.0149

![](mda1_files/figure-gfm/unnamed-chunk-9-5.png)<!-- -->

``` r
cancer_sample %>% ggplot(aes(symmetry_mean, diagnosis)) + ggridges::geom_density_ridges() + ggtitle("Symmetry Mean Density")
```

    ## Picking joint bandwidth of 0.00733

![](mda1_files/figure-gfm/unnamed-chunk-9-6.png)<!-- -->

``` r
cancer_sample %>% ggplot(aes(fractal_dimension_mean, diagnosis)) + ggridges::geom_density_ridges() + ggtitle("Fractal Dimension Mean Density")
```

    ## Picking joint bandwidth of 0.00192

![](mda1_files/figure-gfm/unnamed-chunk-9-7.png)<!-- -->

<!----------------------------------------------------------------------------->

# Task 3: Choose research questions

**(4 points)** So far, you have chosen a dataset and gotten familiar
with it through exploring the data. You have also brainstormed one
research question that interested you (Task 1.4). Now it’s time to pick
4 research questions that you would like to explore in Milestone 2!
Write the 4 questions and any additional comments below.

<!--- *****START HERE***** --->

1.  Is the symmetry and fractal dimension of a tumour related? *These
    are two tumour attributes I am unfamiliar with that I would be
    interested in exploring.*
2.  How well can the diagnosis of a tumour be predicted by its radius,
    texture, smoothness, compactness, concavity, symmetry, and fractal
    dimension? *I am interested in seeing how accurately a diagnosis can
    be predicted based on physical attributes of the tumour.*
3.  Are the worst values of tumour attributes related? (For example, are
    smoothness_worst and concavity_worst related?) *Similarly as in
    research question 1, I am interested in investigating which
    variables are related.*
4.  What is the optimal Logistic regression model to predict diagnosis?
    *It seems natural and useful to me to seek the best prediction model
    for this data.*

<!----------------------------->

# Overall reproducibility/Cleanliness/Coherence Checklist

## Coherence (0.5 points)

The document should read sensibly from top to bottom, with no major
continuity errors. An example of a major continuity error is having a
data set listed for Task 3 that is not part of one of the data sets
listed in Task 1.

## Error-free code (3 points)

For full marks, all code in the document should run without error. 1
point deduction if most code runs without error, and 2 points deduction
if more than 50% of the code throws an error.

## Main README (1 point)

There should be a file named `README.md` at the top level of your
repository. Its contents should automatically appear when you visit the
repository on GitHub.

Minimum contents of the README file:

- In a sentence or two, explains what this repository is, so that
  future-you or someone else stumbling on your repository can be
  oriented to the repository.
- In a sentence or two (or more??), briefly explains how to engage with
  the repository. You can assume the person reading knows the material
  from STAT 545A. Basically, if a visitor to your repository wants to
  explore your project, what should they know?

Once you get in the habit of making README files, and seeing more README
files in other projects, you’ll wonder how you ever got by without them!
They are tremendously helpful.

## Output (1 point)

All output is readable, recent and relevant:

- All Rmd files have been `knit`ted to their output md files.
- All knitted md files are viewable without errors on Github. Examples
  of errors: Missing plots, “Sorry about that, but we can’t show files
  that are this big right now” messages, error messages from broken R
  code
- All of these output files are up-to-date – that is, they haven’t
  fallen behind after the source (Rmd) files have been updated.
- There should be no relic output files. For example, if you were
  knitting an Rmd to html, but then changed the output to be only a
  markdown file, then the html file is a relic and should be deleted.

(0.5 point deduction if any of the above criteria are not met. 1 point
deduction if most or all of the above criteria are not met.)

Our recommendation: right before submission, delete all output files,
and re-knit each milestone’s Rmd file, so that everything is up to date
and relevant. Then, after your final commit and push to Github, CHECK on
Github to make sure that everything looks the way you intended!

## Tagged release (0.5 points)

You’ve tagged a release for Milestone 1.

### Attribution

Thanks to Icíar Fernández Boyano for mostly putting this together, and
Vincenzo Coia for launching.
