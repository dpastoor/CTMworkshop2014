Subsetting
========================================================
author: Devin
width: 1400
height: 900




================

## Accessing columns using $

Can easily call on or manipulate a single column via **dataframe$colname**



```r
head(data$AMT)
```

```
[1] 5000    0    0    0    0    0
```

```r
unique(data$TIME)
```

```
 [1]  0.00  0.25  0.50  1.00  2.00  3.00  4.00  6.00  8.00 12.00 16.00
[12] 24.00
```


================
## Adding Columns to a DF with **$**

```r
# find the mean age and add it to new column
data$MEANAGE <- mean(data$AGE)
head(data, n= 3)
```

```
  ID TIME  AMT   CONC  AGE WEIGHT GENDER     RACE DOSE MEANAGE
1  1 0.00 5000  0.000 56.1   94.2   Male Hispanic 5000   50.52
2  1 0.25    0  8.613 56.1   94.2   Male Hispanic 5000   50.52
3  1 0.50    0 19.437 56.1   94.2   Male Hispanic 5000   50.52
```



================
## Accessing information using **Indexing**

The index is the way that the information can be referenced in the dataframe

* remember **df[row,column]**


```r
data[2,]
```

```
  ID TIME AMT  CONC  AGE WEIGHT GENDER     RACE DOSE
2  1 0.25   0 8.613 56.1   94.2   Male Hispanic 5000
```

```r
head(data[,2], n = 16)
```

```
 [1]  0.00  0.25  0.50  1.00  2.00  3.00  4.00  6.00  8.00 12.00 16.00
[12] 24.00  0.00  0.25  0.50  1.00
```

================ 

## Subsetting

Can easily subset rows of the data frame using the <font color="red">[ ]</font> in combination with <font color="red">$ </font>

```r
ID1 <- data[data$ID == 1,]
ID1
```

```
   ID  TIME  AMT   CONC  AGE WEIGHT GENDER     RACE DOSE
1   1  0.00 5000  0.000 56.1   94.2   Male Hispanic 5000
2   1  0.25    0  8.613 56.1   94.2   Male Hispanic 5000
3   1  0.50    0 19.437 56.1   94.2   Male Hispanic 5000
4   1  1.00    0 34.007 56.1   94.2   Male Hispanic 5000
5   1  2.00    0 30.229 56.1   94.2   Male Hispanic 5000
6   1  3.00    0 31.300 56.1   94.2   Male Hispanic 5000
7   1  4.00    0 24.979 56.1   94.2   Male Hispanic 5000
8   1  6.00    0 23.376 56.1   94.2   Male Hispanic 5000
9   1  8.00    0 23.513 56.1   94.2   Male Hispanic 5000
10  1 12.00    0 14.679 56.1   94.2   Male Hispanic 5000
11  1 16.00    0  9.073 56.1   94.2   Male Hispanic 5000
12  1 24.00    0  5.296 56.1   94.2   Male Hispanic 5000
```

================
## Subsetting (II)
Or can take only a subset of columns

```r
datasmall <- data[, c(1:4)]
```

or using the column names


```r
keepcols <- c("ID", "TIME", "CONC", "AMT")
datasmall <- data[, keepcols]
head(datasmall)
```

```
  ID TIME   CONC  AMT
1  1 0.00  0.000 5000
2  1 0.25  8.613    0
3  1 0.50 19.437    0
4  1 1.00 34.007    0
5  1 2.00 30.229    0
6  1 3.00 31.300    0
```

================
## Using both together


```r
keepcols <- c("ID", "TIME", "CONC", "AMT")
ID1 <- data[data$ID == 1 | data$ID == 5, c("ID", "TIME", "CONC", "AMT")]
head(ID1)
```

```
  ID TIME   CONC  AMT
1  1 0.00  0.000 5000
2  1 0.25  8.613    0
3  1 0.50 19.437    0
4  1 1.00 34.007    0
5  1 2.00 30.229    0
6  1 3.00 31.300    0
```

================
## Multiple subsets

You can also use the **&** and **|** operators to do multiple subsets at once

Let's make a dataset with only males less than 40 years old


```r
youngmales <- data[data$ISM != 0 & data$AGE <= 40,]
head(youngmales[!duplicated(youngmales$CID),])
```

```
[1] ID     TIME   AMT    CONC   AGE    WEIGHT GENDER RACE   DOSE  
<0 rows> (or 0-length row.names)
```

================
## Your Turn
* Subset the dataset into males and females
* Get the summary information for weight for:
  * all individuals
  * and males and females separately
* Challenge:
  * black females and asian males are there? subset out only those groups

================
## Challenge Answer

```r
head(data[(data$RACE == "Black" & data$GENDER == "Female") | (data$RACE == "Asian" & data$GENDER == "Male"),])
```

```
   ID TIME  AMT  CONC   AGE WEIGHT GENDER  RACE DOSE
85  8 0.00 5000  0.00 56.69  85.01   Male Asian 5000
86  8 0.25    0 16.32 56.69  85.01   Male Asian 5000
87  8 0.50    0 22.99 56.69  85.01   Male Asian 5000
88  8 1.00    0 32.43 56.69  85.01   Male Asian 5000
89  8 2.00    0 36.37 56.69  85.01   Male Asian 5000
90  8 3.00    0 44.45 56.69  85.01   Male Asian 5000
```


================
## Subsetting to assign values

What if we needed to change all the 0's in the AMT column to NA values

```r
# so we can keep the original dataset
changedata <- data
head(changedata, n = 3)
```

```
  ID TIME  AMT   CONC  AGE WEIGHT GENDER     RACE DOSE
1  1 0.00 5000  0.000 56.1   94.2   Male Hispanic 5000
2  1 0.25    0  8.613 56.1   94.2   Male Hispanic 5000
3  1 0.50    0 19.437 56.1   94.2   Male Hispanic 5000
```

```r
changedata[changedata$AMT == 0, "AMT"] <- NA
head(changedata, n = 3)
```

```
  ID TIME  AMT   CONC  AGE WEIGHT GENDER     RACE DOSE
1  1 0.00 5000  0.000 56.1   94.2   Male Hispanic 5000
2  1 0.25   NA  8.613 56.1   94.2   Male Hispanic 5000
3  1 0.50   NA 19.437 56.1   94.2   Male Hispanic 5000
```

```r
## or
changedata$AMT[changedata$AMT ==0] <- NA
```

================

## Subsetting with `[` and `[[`

`[` and `[[` are both useful for different tasks. In a general sense you use them to accomplish the following:

|             | Simplifying         | Preserving                 |
|---|---|---|
| Vector      | `x[[1]]`           | `x[1]`                     | 
| List        | `x[[1]]`           | `x[1]`                     | 
| Factor      | `x[1:4, drop = T]`  | `x[1:4]`                   | 
| Array       | `x[1, ]`, `x[, 1]`  | `x[1, , drop = F]`, `x[, 1, drop = F]` | 
| Data frame  | `x[, 1]`, `x[[1]]`  | `x[, 1, drop = F]`, `x[1]` | 

================

An easy way to think about it:

>  "If list `x` is a train carrying objects, then `x[[5]]` is 
> the object in car 5; `x[4:6]` is a train of cars 4-6." 

--- @RLangTip on twitter


================
## Understanding (logical) subsetting

## Logical Subsetting


```r
Theoph[Theoph$Subject ==1,]
```

```
   Subject   Wt Dose  Time  conc
1        1 79.6 4.02  0.00  0.74
2        1 79.6 4.02  0.25  2.84
3        1 79.6 4.02  0.57  6.57
4        1 79.6 4.02  1.12 10.50
5        1 79.6 4.02  2.02  9.66
6        1 79.6 4.02  3.82  8.58
7        1 79.6 4.02  5.10  8.36
8        1 79.6 4.02  7.03  7.47
9        1 79.6 4.02  9.05  6.89
10       1 79.6 4.02 12.12  5.94
11       1 79.6 4.02 24.37  3.28
```

We just subset the Theoph dataframe to only give us back the rows in which Subject equals 1. How does R go about doing this? Logical subsetting!

================


Notice what we get when we simply ask for `Theoph$Subject == 1`

```r
head(Theoph$Subject ==1, n = 50)
```

```
 [1]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
[12] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[23] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[34] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
[45] FALSE FALSE FALSE FALSE FALSE FALSE
```
It doesn't give us back the values for the rows where subject equals one, rather, it gives us back a vector of `TRUE` or `FALSE` values.

So, in reality, we are using the logical subsetting rules to extract the rows of the dataframe that come back `TRUE` from our logical query.


