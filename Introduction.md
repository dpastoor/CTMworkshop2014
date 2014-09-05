---
title: "Introduction"
author: "Devin"
date: "Thursday, August 14, 2014"
output: word_document
---

## Framing the workshop

### Over the course of this workshop we want to use R to:

* Load some data
* calculate basic summary statistics
* visualize the data
* prepare the data for modeling
* modify the data to use for simulations

To do that we'll need to learn some **programming**

### Objectives
* Explain what a library/package is, and what they are used for.
* Load an R library and use the things it contains.
* Learn where to get help
* Read tabular data from a file into a program.
* Assign values to variables.
* Learn about data types

## Getting Started

While we start the overview of R we wanted to make sure everyone has the necessary components set-up for R use. Please open the **setup.R** file and we will show everyone how to run the code. If you have any problems please put up a **RED** sticky and a helper will come assist

--- 

## R Vocabulary
- **packages** are add on features to R that include data, new functions and methods, and extended capabilities. Think of them as ``apps'' on your phone. We've already installed several!
- **terminal** this is the main window of R where you enter commands
- **scripts** these are where you store commands to be run in the terminal later, like syntax files in SPSS or .do files in Stata
- **functions** commands that do something to an object in R
- **data frame** the main data structure used in data analysis, an object with rows and columns that includes numbers, factors, and other data types
- **workspace** the working memory of R where all objects are stored
- **vector** the basic unit of data in R
- **symbols** used to name and store objects or to designate operations/functions
- **attributes** determine how functions act on objects

---

## Components of an R Setup
- **R** - R works in the command line of any OS, but also comes with a basic GUI to operate on its own in Windows and Mac [download](http://cran.r-project.org/)
- **RStudio** - a much better way to work in R that allows editing of scripts, operation of R, viewing of the workspace, and R help all on one screen [download](http://rstudio.com/)

---

## Let's Look at RStudio
- RStudio has made R more accessible and easy to use than ever!
- 4 panels, various tabs
- Help, plots, file structure
- Workspace, history, version control
- Working files
- The R Console

---

## Self-help
- Let's see, type: `?summary`
- For tricky questions, funky error messages (there are many), and other issues, use Google (include "in R" to the end of your query)
- [StackOverflow](http://www.stackoverflow.com) has become a great resource with many questions for many specific packages in R, and a rating system for answers
- A number of R Core members contribute there

---

## Self-help (2)
- Sometimes R Help can be a bit prickly and unfriendly...
- The most important part of getting help is being able to ask your question with a reproducible example (i.e. some short simulated data and code that doesn't do what you want)
- Like this:


```r
Dose <- c(0.1, 0.1, 0.1)
Weight <- c(52, "12", 38)
#Trying to calculate amount to give for weight-based dosing
Dose*Weight
```

In this case, someone could replicate it, allowing them to notice that the '12' is a character rather than numeric and point it out.

- For R Help etiquette (for the tough problems) see [the great advice here](http://adv-r.had.co.nz/Reproducibility.html)


---


## R As A Calculator


```r
2+2 ## add numbers
2*pi #multiply by a constant
7+runif(1,min=0,max=1) #add a random variable
4^4 # powers
sqrt(4^4) # functions
```

---

## Arithmetic Operators
- In addition to the obvious `+` `-` `=` `/` `*` and exponential `^`, there is also integer division `%/%` and remainder in integer division (known as modulo arithmetic) `%%`

```r
2+2
2/2
2*2
2^2
2==2
23 %/% 2 
23 %% 2
```

Note: modulo's are great for simulation read-out updates
---

## Other Key Symbols
- `<-` is the assignment operator, it declares something is something else

```r
ID <-3
ID
```

```
## [1] 3
```

```r
TRT <- "placebo"
TRT
```

```
## [1] "placebo"
```

--- 
## Other Key Symbols (II)
- `:` is the sequence operator

```r
1:10
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

```r
# it increments by one
a<-100:120
a
```

```
##  [1] 100 101 102 103 104 105 106 107 108 109 110 111 112 113 114 115 116
## [18] 117 118 119 120
```
- **This is handy**

---
## Sequence and Repeat
Can have more fine control

```r
#seq(from #, to #, by increment)
seq(0, 24, 0.5)
```

```
##  [1]  0.0  0.5  1.0  1.5  2.0  2.5  3.0  3.5  4.0  4.5  5.0  5.5  6.0  6.5
## [15]  7.0  7.5  8.0  8.5  9.0  9.5 10.0 10.5 11.0 11.5 12.0 12.5 13.0 13.5
## [29] 14.0 14.5 15.0 15.5 16.0 16.5 17.0 17.5 18.0 18.5 19.0 19.5 20.0 20.5
## [43] 21.0 21.5 22.0 22.5 23.0 23.5 24.0
```

```r
#rep (values to repeat, # of times to repeat, ...)
rep(c('a', 'b'), 3)
```

```
## [1] "a" "b" "a" "b" "a" "b"
```

---

## Comments in R
- **#** denotes a comment in R
- Anything after the **#** is not evaluated and ignored in R
- This is handy for making things reproducible


```r
# weight of female adults patients in kg
weight <- c(46.3, 51, 42)
```

---

## R Advanced Math
- R also supports advanced mathematical features and expressions
- R can take integrals and derivatives and express complex functions
- Easiest of all, R can generate distributions of data very easily

  - e.g. `rnorm(100)` or `rbinom(100)`

- This comes in handy when writing examples and building analyses because it is trivial to generate a synthetic piece of data to use as an example
- Try typing `hist(rnorm(10000))`

---

## Using the Workspace
- To do more we need to learn how to manipulate the 'workspace'.
- This includes all the vectors, datasets, and functions stored in memory.
- All R objects are stored in the memory of the computer, limiting the available space for calculation to the size of the RAM on your machine.
- R makes organizing the workspace easy.

---

## Using the Workspace (2)
```
x<-5 #store a variable with <-
x    #print the variable
z<-3 
ls() #list all variables
ls.str() #list and describe variables
rm(x)    # delete a variable
ls()
```
You can also also visually see what is in your workspace in Rstudio

---

## Concatenating with `c`
- So what does **c** do?

```r
A<-c(3,4)
print(A)
```

```
## [1] 3 4
```
- `c` stands for concatenate and allows vectors to have multiple elements
- If you ever need two elements in a vector, you need to wrap it up in `c`, which is one of the most used functions you will ever use
- `c` is important to put any vector together, but remember that *objects within a vector must all be of the same type*

---

## Some Other Language ~~Bugs~~ Features
- R is maddeningly inconsistent in it's naming conventions
  * Some functions are `camelCase`; others `are.dot.separated`; others `use_underscores`
  * Function results are stored in a variety of ways across function implementations
  * R has multiple graphics packages that different functions use for default plot construction (`base`, `grid`, `lattice`, and `ggplot2`)
  * R has multiple packages and functions to do the same analysis as well, though some standardization has started to occur
  * Be flexible and be aware of R's flexibility


---

## Special Operators
- The comparison operators `<`, `>`, `<=`, `>=`, `==`, and `!=` are used to compare values across values or vectors



```r
large_dose <- 1000
small_dose <- 100
large_dose > small_dose
```

```
## [1] TRUE
```

---

## Using Vectors

```r
bigger_values <-c(9,12,15,25)
smaller_values<-c(9,3,4,2)
# Give us a nice vector of logical values
bigger_values>smaller_values
```

```
## [1] FALSE  TRUE  TRUE  TRUE
```

```r
bigger_values=smaller_values

# Oops--don't do this, reassigns big to small
print(bigger_values)
```

```
## [1] 9 3 4 2
```
- Comparison operators can be tricky, so to keep it straight never use `=` or `==` to assign anything, always use `<-`

---

## Special operators (II)
- The logical operators `|` (or) and `&` (and) can be used to combine two logical values and produce another logical value as the result. The operator `!` (not) negates a logical value. These operators allow complex conditions to be constructed.


```r
foo<-c(NA,4,9,8.7)
!is.na(foo) # Returns TRUE for non-NA
```

```
## [1] FALSE  TRUE  TRUE  TRUE
```

```r
a <-foo[!is.na(foo)]
a
```

```
## [1] 4.0 9.0 8.7
```


---
## Data Structures in R

## Data Structures

R has a number of ways of storing information. The quick way to visualize the possibilities is as such:

|    | Homogeneous    | Heterogeneous |
|----|---------------|--------------|
| 1d | Atomic vector | List         |
| 2d | Matrix        | Data frame   |
| nd | Array         |              |

**Homogeneous** - all elements must be of the same type 
**Heterogeneous** - elements can be of different type

---

## Data types

A **Type/Mode** indicates how R stores the information in memory
* numeric
* double
* integer
* logical
* character
* list of pointers
* function


---
- R has a number of basic data classes as well as arbitrary specialized object types for various purposes
- **vectors** are the basic data class in R and can be thought of as a single column of data (even a column of length 1)
- **matrices and arrays** are rows and columns of all the same mode data
- **data frames** are rows and columns where the columns can represent different data types
- **lists** are arbitrary combinations of disparate object types in R

There are two useful functions for handling vectors: `is.*` and `as.*`

* `is.*` is a testing function that returns TRUE or FALSE
* `as.*` is a coercion function - it attempts to convert the input to the requested data structure

---

## Working with Vectors


```r
# example vector
numeric_vector <- c(1, 2, 3)

# access contents by calling the vector by name
numeric_vector
```

```
## [1] 1 2 3
```

```r
# see vector type
typeof(numeric_vector)
```

```
## [1] "double"
```

```r
# often more useful than typeof
str(numeric_vector)
```

```
##  num [1:3] 1 2 3
```

```r
# check length
length(numeric_vector)
```

```
## [1] 3
```

---

## Coercion

For homogeneous vectors, if you attempt to combine elements of different types, it will pick the class of the first element and coerce all others to that type


```r
vec <- c("2", 3, 4)
2 > vec
```

```
## [1] FALSE FALSE FALSE
```

```r
# logical TRUE == 1
vec <- c("2", 1, 4)
2 > vec
```

```
## [1] FALSE  TRUE FALSE
```

## when might you run into this in a PM-style dataset?

---
## Working with data frames
class(data)

- Data frames are uniform in shape and information inside a column - this makes it easy to work with!
- **[ ]**'s are an easy way to get to certain parts of a data frame
- A data frame is written as: **data[row, column]**
- each column is a vector (homogenous)
- a dataframe is "essentially" a list with equal length columns


---

# PULSE CHECK

---
## Reading in Data

Data from a variety of formats an be read into R - two of the most common are .tab and .csv

Any text with a separator can be passed into read.csv or read.table regardless of file ending (.sim, etc)

* `read.csv`
* `read.table`

---
```
## Let's read in some data
We can quickly find additional information about the dataset

```r
library(PKPDdatasets)
```

```
## Error: there is no package called 'PKPDdatasets'
```

```r
data <- read.csv("datasets//richPK.csv")
# What are the column names?
names(data)
```

```
## [1] "ID"     "Time"   "Amt"    "Conc"   "Age"    "Weight" "Gender" "Race"  
## [9] "Dose"
```

```r
# how long is the dataset - did everything read in correctly?
nrow(data)
```

```
## [1] 600
```

```r
# numer of columns
ncol(data)
```

```
## [1] 9
```

---


```r
#What is the structure of each column
str(data)
```

```
## 'data.frame':	600 obs. of  9 variables:
##  $ ID    : int  1 1 1 1 1 1 1 1 1 1 ...
##  $ Time  : num  0 0.25 0.5 1 2 3 4 6 8 12 ...
##  $ Amt   : int  5000 0 0 0 0 0 0 0 0 0 ...
##  $ Conc  : num  0 8.61 19.44 34.01 30.23 ...
##  $ Age   : num  56.1 56.1 56.1 56.1 56.1 ...
##  $ Weight: num  94.2 94.2 94.2 94.2 94.2 ...
##  $ Gender: Factor w/ 2 levels "Female","Male": 2 2 2 2 2 2 2 2 2 2 ...
##  $ Race  : Factor w/ 5 levels "Asian","Black",..: 4 4 4 4 4 4 4 4 4 4 ...
##  $ Dose  : int  5000 5000 5000 5000 5000 5000 5000 5000 5000 5000 ...
```

```r
# capitalize all the names
names(data) <- toupper(names(data))
names(data)
```

```
## [1] "ID"     "TIME"   "AMT"    "CONC"   "AGE"    "WEIGHT" "GENDER" "RACE"  
## [9] "DOSE"
```

---

We can get some summary information


```r
summary(data)
```

```
##        ID            TIME             AMT            CONC      
##  Min.   : 1.0   Min.   : 0.000   Min.   :   0   Min.   :  0.0  
##  1st Qu.:13.0   1st Qu.: 0.875   1st Qu.:   0   1st Qu.: 13.3  
##  Median :25.5   Median : 3.500   Median :   0   Median : 29.9  
##  Mean   :25.5   Mean   : 6.396   Mean   : 417   Mean   : 32.8  
##  3rd Qu.:38.0   3rd Qu.: 9.000   3rd Qu.:   0   3rd Qu.: 48.0  
##  Max.   :50.0   Max.   :24.000   Max.   :5000   Max.   :130.7  
##       AGE           WEIGHT        GENDER           RACE          DOSE     
##  Min.   :38.3   Min.   :54.9   Female:180   Asian    : 84   Min.   :5000  
##  1st Qu.:46.6   1st Qu.:64.2   Male  :420   Black    :144   1st Qu.:5000  
##  Median :50.8   Median :71.2                Caucasian:156   Median :5000  
##  Mean   :50.5   Mean   :71.0                Hispanic : 96   Mean   :5000  
##  3rd Qu.:54.5   3rd Qu.:76.9                Other    :120   3rd Qu.:5000  
##  Max.   :60.6   Max.   :94.2                                Max.   :5000
```

---

# Your Turn

Using the provided `R cheatsheet` what commands would likely help you solve the following

* How many rows are in the dataset
* The number of *unique* IDs
* The *range* of ages




