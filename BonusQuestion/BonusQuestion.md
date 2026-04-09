# 1 notes on the recap material

These questions focus on material that students commonly struggle with
(data wrangling, plotting, modeling, or debugging).

Ans: Data wrangling (dplyr) Select () chooses columns Filter() keeps
rows based on conditions Mutate() create new variables Summarise ()
reduces data to summary statistics Group_by() groups data before
summarizing Always check column names and data types before wrangling

Examples; library(dplyr)

data_summary \<- df %\>% filter(year == 2025) %\>% group_by(treatment)
%\>% summarise(mean_yield = mean(yield, na.rm = TRUE))

Common mistakes: summarise without group_by wrong column names factors
vs numeric mismatch

Plotting (ggplot2)

Basic structure:

ggplot(data, aes(x, y)) + geom_point()

Common layers:

geom_point() scatter plot geom_line() line plot
geom_bar(stat=“identity”) bar chart facet_wrap(~variable) multiple plots
theme_classic() clean theme

Example:

ggplot(df, aes(treatment, yield)) + geom_boxplot() + theme_classic()

Common mistakes:

mapping inside vs outside aes() forgetting + wrong variable names
plotting summarized data incorrectly Linear modeling

Basic model:

model \<- lm(yield ~ treatment, data = df) summary(model)

Important outputs:

Estimate = effect size p-value = significance R² = model fit Residuals =
model error

Prediction:

predict(model)

Common mistakes:

response and predictor reversed categorical variables not converted to
factor missing values in model data Debugging

Steps:

read the error message carefully run code line-by-line check object
names check parentheses and commas use View(df) or str(df) print
intermediate outputs

Example:

str(df) names(df)

### Pipes %\>%

Confusing library(tidyverse) microbiome.fungi \<-
read.csv(file.choose()) str(microbiome.fungi) microbiome.fungi2 \<-
select(microbiome.fungi, SampleID, Crop, Compartment:Fungicide,
richness) str(microbiome.fungi2) head(filter(microbiome.fungi2,
Treatment == “Conv.”)) microbiome.fungi %\>% select(SampleID, Crop,
Compartment:Fungicide, richness) %\>%  
filter(Treatment == “Conv.”) %\>%  
mutate(logRich = log(richness)) %\>%  
head()


    ### Grouping and summarising
    confusing
    ``{r} 
    microbiome.fungi %>%
      select(SampleID, Crop, Compartment:Fungicide, richness) %>%
      group_by(Treatment, Fungicide) %>%        # define groups
      mutate(logRich = log(richness)) %>%       # uses groups but keeps rows
      summarise(Mean.rich = mean(logRich),      # 1 row per group
                n = n(),
                sd.dev = sd(logRich)) %>%
      mutate(std.err = sd.dev / sqrt(n))

    # 2  explore a topic of your choice

    Ans: I chose to explore pivot_longer() because reshaping data from wide to long format is often required before plotting and modeling. I wanted to understand how to convert multiple measurement columns into tidy format usable in ggplot and dplyr workflows. 

    Example: 


    library(tidyr)

    long_df <- df %>%
    pivot_longer(cols = starts_with("rep"),
    names_to = "replicate",
    values_to = "value")

    It is useful to
    •   Easier plotting
    •   Easier grouping
    •   Tidy data structure


    also;
    I chose to explore how to plot graphs in R using ggplot2. I picked this topic because plotting is essential for exploring and communicating patterns in data, and I want to become more comfortable creating clear, publication-quality figures. 


    library(ggplot2)

    ggplot(mtcars, aes(x = wt, y = mpg, color = factor(cyl))) + 
      geom_point(size = 2) +
      geom_smooth(method = "lm", se = TRUE) +
      labs(
        title = "MPG vs Weight by Cylinders",
        x = "Weight (1000 lbs)",
        y = "Miles per gallon",
        color = "Cylinders"
      ) +
      theme_minimal()

I wanted to learn how each piece of the code works: how aes() maps
variables to x, y, and color, how geom_point() and geom_smooth() stack
as layers, and how functions like labs() and theme_minimal() change the
non-data elements of the graph to improve readability.

# 3 Introduction to renv.

• Follow the coding demonstration in class. Turn in notes.

Ans: renv Notes: renv is an R package for project‑specific package
libraries that improves reproducibility and portability. It creates a
local library folder for each project plus a renv.lock file that records
exact package names and versions used.

Purposes: • creates Reproducible R environments • tracks package
versions • allows others to run code without errors

Initialize project:

``` r
install.packages("renv")
```

    ## - Querying repositories for available source packages ... Done!
    ## The following package(s) will be installed:
    ## - renv [1.2.0]
    ## These packages will be installed into "~/Reproducibility-GB/BonusQuestion/renv/library/windows/R-4.4/x86_64-w64-mingw32".
    ## 
    ## # Downloading packages -------------------------------------------------------
    ## [?25l  (0/1) Downloading: renv                                                                                                                                       [32m✔[0m renv 1.2.0                               [2.5 MB in 2.3s]
    ##                                                                                 Successfully downloaded 1 package in 3.6 seconds.
    ## 
    ## # Installing packages --------------------------------------------------------
    ## [32m✔[0m renv 1.2.0                               [installed binary in 0.73s]
    ## Successfully installed 1 package in 1.2 seconds.
    ## [?25h

``` r
renv::init()
install.packages("dplyr")
```

    ## The following package(s) will be installed:
    ## - dplyr      [1.2.1]
    ## - generics   [0.1.4]
    ## - glue       [1.8.0]
    ## - magrittr   [2.0.5]
    ## - pillar     [1.11.1]
    ## - pkgconfig  [2.0.3]
    ## - R6         [2.6.1]
    ## - rlang      [1.2.0]
    ## - tibble     [3.3.1]
    ## - tidyselect [1.2.1]
    ## - utf8       [1.2.6]
    ## - vctrs      [0.7.2]
    ## - withr      [3.0.2]
    ## These packages will be installed into "~/Reproducibility-GB/BonusQuestion/renv/library/windows/R-4.4/x86_64-w64-mingw32".
    ## 
    ## # Downloading packages -------------------------------------------------------
    ## [?25l  (0/5) Downloading: tidyselect, magrittr, generics, dplyr, ...                                                                                                 [32m✔[0m generics 0.1.4                           [85 kB in 0.4s]
    ##   (1/5) Downloading: tidyselect, magrittr, dplyr, rlang                                                                                                         [32m✔[0m magrittr 2.0.5                           [228 kB in 0.65s]
    ##   (2/5) Downloading: tidyselect, dplyr, rlang                                                                                                                   [32m✔[0m tidyselect 1.2.1                         [230 kB in 0.93s]
    ##   (3/5) Downloading: dplyr, rlang                                                                                                                               [32m✔[0m rlang 1.2.0                              [1.6 MB in 2.8s]
    ##   (4/5) Downloading: dplyr                                                                                                                                      [32m✔[0m dplyr 1.2.1                              [1.6 MB in 3.5s]
    ##                                                                                 Successfully downloaded 5 packages in 4 seconds.
    ## 
    ## # Installing packages --------------------------------------------------------
    ## [32m✔[0m R6 2.6.1                                 [linked from cache]
    ## [32m✔[0m withr 3.0.2                              [linked from cache]
    ## [32m✔[0m pillar 1.11.1                            [linked from cache]
    ## [32m✔[0m glue 1.8.0                               [linked from cache]
    ## [32m✔[0m tibble 3.3.1                             [linked from cache]
    ## [32m✔[0m utf8 1.2.6                               [linked from cache]
    ## [32m✔[0m vctrs 0.7.2                              [linked from cache]
    ## [32m✔[0m pkgconfig 2.0.3                          [linked from cache]
    ## [32m✔[0m dplyr 1.2.1                              [installed binary in 0.71s]
    ## [32m✔[0m generics 0.1.4                           [installed binary in 0.87s]
    ## [32m✔[0m magrittr 2.0.5                           [installed binary in 0.99s]
    ## [32m✔[0m rlang 1.2.0                              [installed binary]
    ## [32m✔[0m tidyselect 1.2.1                         [installed binary]
    ## Successfully installed 13 packages in 5.5 seconds.
    ## [?25h
    ## The following loaded package(s) have been updated:
    ## - rlang
    ## Restart your R session to use the new versions.

``` r
renv::snapshot()
```

    ## The following package(s) will be updated in the lockfile:
    ## 
    ## # CRAN -----------------------------------------------------------------------
    ## - R6      [2.5.1 -> 2.6.1]
    ## - rlang   [1.1.6 -> 1.2.0]
    ## 
    ## - Lockfile written to "~/Reproducibility-GB/BonusQuestion/renv.lock".

``` r
renv::restore()
```

    ## - The library is already synchronized with the lockfile.

Files created:

renv.lock → package versions renv/ folder → project library

It is important because:

ensures reproducibility avoids package conflicts allows project sharing
