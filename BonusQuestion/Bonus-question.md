# 1

Give me notes on the recap material. These questions focus on material
that students commonly struggle with (data wrangling, plotting,
modeling, or debugging). Ans: Data wrangling (dplyr) Select () chooses
columns Filter() keeps rows based on conditions Mutate() create new
variables Summarise () reduces data to summary statistics Group_by()
groups data before summarizing Always check column names and data types
before wrangling

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

# 2

Complete one of the extra optional materials provided, OR explore a
topic of your choice, or find a topic online and explore the code and
how it works. Ans: I chose to explore pivot_longer() because reshaping
data from wide to long format is often required before plotting and
modeling. I wanted to understand how to convert multiple measurement
columns into tidy format usable in ggplot and dplyr workflows. Example:
library(tidyr)

long_df \<- df %\>% pivot_longer(cols = starts_with(“rep”), names_to =
“replicate”, values_to = “value”) It is useful to • Easier plotting •
Easier grouping • Tidy data structure

# 3

Introduction to renv. • Follow the coding demonstration in class. Turn
in notes.

Ans: renv Notes Purposes: • creates Reproducible R environments • tracks
package versions • allows others to run code without errors

Initialize project:

install.packages(“renv”) renv::init()

Install packages:

install.packages(“dplyr”)

Snapshot packages:

renv::snapshot()

Restore environment:

renv::restore()

Files created:

renv.lock → package versions renv/ folder → project library

It is important because:

ensures reproducibility avoids package conflicts allows project sharing
