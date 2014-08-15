grouping_reshaping
========================================================
author: Devin Pastoor
date: 
width:1400
height: 900

====================
## One (summarization) package to rule them all?
* built in functions like aggregate and the old (but still useful) package plyr make group summary statistics easy
* **dplyr** makes everything a breeze

====================
## Key dplyr Functions
* filter: keeps rows with matching criteria
* summarize: do calculations *and* reduce resulting variables and values
* mutate: do calculations *and* add them to existing data frame
* arrange: ordering
* select: picking columns by name

#### wrapped with `%>%` and tied with a `group_by` bow


====================
# What does is look like




```r
data %>% 
  group_by(ID) %>% 
    summarize(cmax = max(CONC)) %>% 
      head
```

```
Source: local data frame [6 x 2]

  ID   cmax
1  1  34.01
2  2 100.18
3  3  53.86
4  4  96.68
5  5  51.63
6  6  27.94
```


=============================


# Go to dplyr handson

====================


# Reshaping Data

There is an excellent package (library) called reshape2


```r
library(reshape2)
dat_10IDS <- data %>% filter(ID < 10)
m_dat_10IDS <- melt(dat_10IDS %>% 
                      select(ID,TIME, AMT, CONC, 
                             AGE, WEIGHT, DOSE), 
                    id.vars="ID")
```

===============================

```r
head(m_dat_10IDS, n = 15)
```

```
   ID variable value
1   1     TIME  0.00
2   1     TIME  0.25
3   1     TIME  0.50
4   1     TIME  1.00
5   1     TIME  2.00
6   1     TIME  3.00
7   1     TIME  4.00
8   1     TIME  6.00
9   1     TIME  8.00
10  1     TIME 12.00
11  1     TIME 16.00
12  1     TIME 24.00
13  2     TIME  0.00
14  2     TIME  0.25
15  2     TIME  0.50
```
***

```r
tail(m_dat_10IDS, n = 15)
```

```
    ID variable value
634  8     DOSE  5000
635  8     DOSE  5000
636  8     DOSE  5000
637  9     DOSE  5000
638  9     DOSE  5000
639  9     DOSE  5000
640  9     DOSE  5000
641  9     DOSE  5000
642  9     DOSE  5000
643  9     DOSE  5000
644  9     DOSE  5000
645  9     DOSE  5000
646  9     DOSE  5000
647  9     DOSE  5000
648  9     DOSE  5000
```




====================
## What about long to wide
How can we make a table of concentrations by time for all ID's? (long to wide conversion)


```r
molten <- melt(data %>% filter(ID < 6), id.vars = c("TIME", "ID"), measure.vars = c("CONC"))
```

====================

```r
head(molten)
```

```
  TIME ID variable  value
1 0.00  1     CONC  0.000
2 0.25  1     CONC  8.613
3 0.50  1     CONC 19.437
4 1.00  1     CONC 34.007
5 2.00  1     CONC 30.229
6 3.00  1     CONC 31.300
```
***

```r
tail(molten)
```

```
   TIME ID variable  value
55    4  5     CONC 49.138
56    6  5     CONC 25.564
57    8  5     CONC 24.368
58   12  5     CONC 17.265
59   16  5     CONC  8.935
60   24  5     CONC  3.563
```

======================



```r
concTimeWide <- dcast(molten, TIME + variable ~ ID)
head(concTimeWide, n = 20)
```

```
    TIME variable      1      2      3     4      5
1   0.00     CONC  0.000   0.00  0.000  0.00  0.000
2   0.25     CONC  8.613  30.40 16.950 29.30 17.620
3   0.50     CONC 19.437  47.63 24.384 50.49 28.704
4   1.00     CONC 34.007  64.43 50.325 66.45 46.769
5   2.00     CONC 30.229 100.18 53.461 88.99 51.631
6   3.00     CONC 31.300  92.56 53.858 75.06 50.831
7   4.00     CONC 24.979  65.27 45.887 96.68 49.138
8   6.00     CONC 23.376  49.26 32.861 56.20 25.564
9   8.00     CONC 23.513  60.29 22.889 66.60 24.368
10 12.00     CONC 14.679  44.25 13.789 38.97 17.265
11 16.00     CONC  9.073  41.85  6.692 43.62  8.935
12 24.00     CONC  5.296  32.90  2.336 26.17  3.563
```
