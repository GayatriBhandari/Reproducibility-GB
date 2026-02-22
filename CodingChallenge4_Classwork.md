# Question

*In the context of R Markdown , the YAML header appears at the top of
the document, enclosed by — lines, and it contains metadata about the
document.* *Literate Programming(For eg. R Markdown) is documentation
and code live together in the same file, making it easy for others (and
your future self!) to understand not just what the code does, but why it
was written that way.*

# Question2a

\-[PaperLink](https://apsjournals.apsnet.org/doi/10.1094/PDIS-06-21-1253-RE)

# Question2b

``` r
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 4.4.3

    ## Warning: package 'ggplot2' was built under R version 4.4.3

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   4.0.2     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(ggplot2)
library(ggpubr) 
```

    ## Warning: package 'ggpubr' was built under R version 4.4.3

``` r
mycotoxin<- read.csv(file.choose())
mycotoxin$Treatment <- as.factor(mycotoxin$Treatment) 
mycotoxin$Cultivar <- as.factor(mycotoxin$Cultivar)  
str(mycotoxin)
```

    ## 'data.frame':    375 obs. of  6 variables:
    ##  $ Treatment     : Factor w/ 5 levels "Fg","Fg + 37",..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ Cultivar      : Factor w/ 2 levels "Ambassador","Wheaton": 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ BioRep        : int  2 2 2 2 2 2 2 2 2 3 ...
    ##  $ MassperSeed_mg: chr  "10.29130435" "12.80322581" "2.846666667" "6.5" ...
    ##  $ DON           : chr  "107.3" "32.6" "416" "211.9" ...
    ##  $ X15ADON       : chr  "3" "0.85" "3.5" "3.1" ...

# Question2c

``` r
cbbPalette <- c("#56B4E9", "#009E73")
```

# DON_PLOT1

``` r
Plot1 <- ggplot(mycotoxin, aes(x = Treatment, y = DON, fill = Cultivar)) + 
  geom_boxplot(position = position_dodge(0.85)) + 
  xlab("") +  
  ylab("DON (ppm)") + 
  geom_point(alpha = 0.6,pch = 21, color = "black") + 
  scale_fill_manual(values = cbbPalette)+ 
  facet_wrap(~Cultivar)+  
  theme_classic() 
Plot1
```

![](CodingChallenge4_Classwork_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

# Plot X15ADON

``` r
Plot2 <- ggplot(mycotoxin, aes(x = Treatment, y = X15ADON, fill = Cultivar)) + 
  geom_boxplot(position = position_dodge(0.85)) +  
  xlab("") +  
  ylab("15ADON") +  
  geom_point(alpha = 0.6,pch = 21, color = "black") + 
  scale_fill_manual(values = cbbPalette)+ 
  facet_wrap(~Cultivar)+ 
  theme_classic() 
Plot2
```

![](CodingChallenge4_Classwork_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

# SeedMass

``` r
#Plot 3

Plot3<- ggplot(mycotoxin, aes(x = Treatment, y = MassperSeed_mg, fill = Cultivar)) + 
geom_boxplot(position = position_dodge(0.85)) +  
  xlab("") +  
  ylab("Seed Mass (mg)") +  
  geom_point(alpha = 0.6,pch = 21, color = "black") + 
  scale_fill_manual(values = cbbPalette)+ 
  facet_wrap(~Cultivar)+ 
  theme_classic() 
Plot3
```

![](CodingChallenge4_Classwork_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

# Question5

[README](%22CodingChallenge4_Classwork.md%22)

# Question6

[Github](https://github.com/GayatriBhandari/Reproducibility-GB.git)
