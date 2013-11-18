---
title       : R Intro Part IV
subtitle    : Data structures and functions
author      : Ilan Man
job         : Data Analytics at Squarespace
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
---

## Agenda 

1. Intro
2. Data structures
3. Control Structures
4. Functions
5. Commonly used built in functions
6. String Manipulation

----

## Intro

- Background
- Styling

----

## Intro
Background

- Derivative of S language. Developed at Bell Laboratories
- Open source (Revolution Analytics offers commerical software)
- Originally command line, but RStudio becoming more popular
- Very popular, especially among academics and statisticians
- Intepreted language - easier to write code, but slower computations
- Packages available to speed up R code - `xts`, `Rcpp`, `Rprof`
- R holds all data in RAM. Problematic for large data sets.
- R is excellent for prototyping

----

## Intro
Background

- Installing packages

```r
install.packages('ggplot2')    ## do this once only
require('ggplot2')             ## do this every time you load up an R session

library()                      ## shows you every package in your standard package location
```

----

## Intro
Styling

- CRAN and Google style guide
- Use `<-` NOT `=` for assignment
- Spaces between operators like `+`, `%*%`, `<`, `>` and after closing brackets `)`, `}`
- Don't write functions named `rep()`, `sample()`, `plot()` or any other built-in R names
- Use camel case for functions: `myFirstFunction()` is better than `my.first.function()`
- Styling resources:
  <ul>[CRAN](http://cran.r-project.org/web/packages/rockchalk/vignettes/Rstyle.pdf)</ul>
  <ul>[Google](http://google-styleguide.googlecode.com/svn/trunk/Rguide.xml)</ul>
  <ul>[R Coding convention](https://docs.google.com/document/d/1esDVxyWvH8AsX-VJa-8oqWaHLs4stGlIbk8kLc5VlII/edit)</ul>


----

## Data structures

1. Vectors
2. Matrices
3. Lists
4. Data.frames
5. Factors

----

## Data structures
Vectors

- Fundamental R data type: Everything is a vector in R (including scalars)
- Vector elements must be of the same type, or `mode` in R
- Common ways to initialize a vector

```r
x <- c(1,2,3,4,5,6,7,8,9,10) ## vector from 1 to 10 - class numeric
x <- 1:10                    ## alternative - class integer
x <- seq(from=1,to=10,by=1)  ## alternative - class numeric

n <- 10
x <- numeric(n)
for (i in 1:n) x[i] <- i    ## as n gets large, this is very slow (compared to the 
                            ## alternatives)
x <- numeric(0)             
for (i in 1:n) x <- c(x,i)  ## to the extent possible, provide the size of your object when
                            ## initializing it
```

----

## Data structures
Vectors

- Vectors obviate need for loops (most of the time!)


```r
x <- seq(from = 1, to = 10, by = 1)
for (i in c(1:length(x))) y[i] <- x[i] * 5
y
```

```
##    [1]  5.00000 10.00000 15.00000 20.00000 25.00000 30.00000 35.00000
##    [8] 40.00000 45.00000 50.00000  0.11447  7.52623 19.51378 14.83657
##   [15]  6.03286 13.41995 19.43599  6.11456 14.72639 17.77366 17.61540
##   [22]  5.66113  4.96782  6.08313  8.79416  4.32664 13.46208 10.59188
##   [29] 18.85593  7.42452  0.31533 12.32764  7.69819 10.98761  6.54966
##   [36]  4.88192 12.27283 14.80577 12.01640  5.19024  7.36981  8.14746
##   [43] 10.24839 15.66229 17.52268 16.36622  8.72764 18.43468 11.41363
##   [50] 14.27011  8.40666  9.51449 10.52563 10.29971  6.27028  8.17921
##   [57] 14.07263  1.67730  6.68097  6.83003 19.19556 10.36491  2.15994
##   [64]  5.15862  2.10022  8.97148  3.55940  4.48527 15.76575 15.43147
##   [71]  1.17183 13.75970  2.80312  0.29010  9.31030  9.45745  1.16149
##   [78]  2.62275 12.41009 11.69492  2.53246 18.43957 11.86537 14.10834
##   [85]  2.30606 13.47979 18.94206 18.35539  3.93877 14.80280  8.03977
##   [92]  9.44826  1.86189 17.40273  5.01379 19.11841 12.57419 13.56184
##   [99] 14.92179  9.85681 17.75135 19.06699 10.82559 16.49191  6.60909
##  [106]  3.63201  5.68065 12.56396  2.54818 18.88470 11.33552  7.03587
##  [113]  5.03473  5.72405  0.32186 18.35864 13.23285 15.44570  1.00982
##  [120]  8.97853  7.46232  7.62874 15.78574  9.70140 19.86718  0.22659
##  [127]  2.92240  3.76685  8.61803  9.62963  8.12508  7.16669  0.60863
##  [134] 17.84764  0.05266  5.46688  9.84322  5.59559 15.16929  4.52378
##  [141] 13.28804  0.98721 19.40430  1.42293 13.78190  3.46946 12.62344
##  [148]  7.00417 17.84908  6.16081 10.80373  0.59946  6.70434 18.82350
##  [155] 10.04613  6.99272 14.45274  6.96988  3.96013 18.34789 10.34008
##  [162] 13.54067  5.21074  3.02062 10.29014  5.70189 14.67398 12.35411
##  [169] 17.66432  3.15842  8.42191  1.93714  8.46169 12.73824 13.59329
##  [176]  4.42640  9.32954  1.22258  5.26587  5.26156 19.59000 11.12404
##  [183] 19.69454  2.18785  6.07035  8.51891 13.71808  8.23243 11.85938
##  [190]  8.31908 12.25347 14.08142  7.69905 14.31664  1.93091 12.05601
##  [197]  2.20210 14.56854  8.65802  9.21816  4.46059  4.84693 16.95929
##  [204]  7.13370 14.49232 18.80931 18.70087 11.40779 11.20720 16.26144
##  [211] 17.33472 10.65800  3.01266 16.78857 16.78444 15.89825 11.30137
##  [218]  3.04192 17.19422  7.61910  5.02100  1.25796  2.55325  4.78753
##  [225] 14.46163 10.39573  9.47339  3.61486 19.20500  8.86357  2.83990
##  [232] 13.61108 10.63601 15.23437 11.21294 12.17389 16.94811  8.88514
##  [239]  2.87115  2.96657 10.78067  6.55099  2.20479 13.31488 11.03723
##  [246] 17.18167  4.62396 10.55507  2.85142  8.68125  9.21000  8.77673
##  [253] 10.22377  2.35606  9.59589 17.09822 15.78655  5.52629  6.05287
##  [260]  1.83423  1.23956  5.71947 19.96764  0.53278  4.99113 14.82505
##  [267]  5.58204 11.87756  6.78880 10.97083  5.68204 19.23505  4.72111
##  [274] 10.67042 13.47877 13.23406 13.92078  7.30588  5.80799 17.47478
##  [281] 15.26590 10.04800  9.64812  0.38938  3.59033  2.68983 17.56170
##  [288]  8.61500 11.74188  2.87368 11.28692  7.41583 12.83173  3.53887
##  [295] 18.19341  4.77667 18.66934 14.37972  5.94104  2.83128 11.31146
##  [302]  0.91694  9.38834 12.71365 11.54109  0.88074  4.49048 15.98760
##  [309]  3.17411  3.51603  8.43318  1.20140  2.01741 12.93191 18.22102
##  [316]  1.91076  0.45068 14.13714 12.85312 19.60831 12.57436  1.01637
##  [323] 12.03727 19.03037 11.59113  6.68320  3.84764 14.22015  3.96961
##  [330] 12.58373 14.10106 13.09739 19.62476 15.93812 16.39624  3.19585
##  [337] 11.90473 14.03600  9.20341  5.94983  2.97268 13.28203  3.50794
##  [344]  2.44792 17.14234  1.29791 15.57199 14.51209  8.55839  9.18484
##  [351]  3.40801 16.68584 15.11210 16.87414 19.72361 16.39609 15.56176
##  [358]  2.70101  2.75364  2.99870 16.37728 18.30447 16.15268  1.40039
##  [365]  0.82266  7.15843 16.03296 11.63652 18.01515  9.68507  0.74861
##  [372] 16.75114  0.33875 14.51566  6.88279  3.62752  2.74966  2.58358
##  [379]  6.94898 10.03415 13.51288 10.31225  4.59284 12.11585 12.14711
##  [386]  1.62154  6.67198  9.00359  4.95865  5.81522 14.29729 15.47925
##  [393] 17.13706  4.21839 12.11458 14.15386  3.72363  3.87682  1.76423
##  [400]  0.56996 15.63178 10.23246  1.23097 17.04093 12.65701  3.17498
##  [407] 12.19914 16.93621 16.88198 18.41120 16.30990  0.98873  1.45935
##  [414] 16.49321 10.20222 14.29568 16.90779 17.93222  8.71556  0.17642
##  [421] 16.54851  2.16697 16.25813  4.90565 10.12404 14.40231  3.61460
##  [428]  1.48198  5.07850 17.49209  6.48174  7.10631  2.27279 11.31548
##  [435]  8.41394 13.98002 12.84032  6.92242 19.05383 12.66557  4.14700
##  [442] 15.46178  4.80988  8.22215 14.32031 14.06789 15.04474 19.50328
##  [449] 16.61905  5.80414 14.16747  0.42107 17.41899  1.65109 17.13878
##  [456]  4.00044 18.52881  5.61667 15.57237 12.72822 16.24887 16.37200
##  [463] 12.75422  0.43239  7.63569  2.72184  6.56046  7.56634 19.56218
##  [470]  4.97760  5.42557  8.57690  0.35108 16.01514 15.15891 12.86454
##  [477] 11.40159 17.04493  7.63210 16.86676  1.18386 10.95470 10.35964
##  [484] 15.56067  0.35731  4.26453  9.74940 17.71960 14.03984 11.51922
##  [491]  4.92655  4.42011  5.12947  5.26077 18.85574  4.18055  7.70811
##  [498]  1.25019 12.63667  7.19464  5.00391 16.43727  1.24114 19.85924
##  [505]  7.76974  3.95069 14.23357 14.55701 14.30311  6.81934 12.91129
##  [512]  5.21411 19.44752  8.93485 15.31527  1.63835 18.50221 13.14521
##  [519]  5.66685  9.63587  4.91335 19.18704 11.52596  8.20527  2.46833
##  [526] 11.26936  5.05156 19.41680  3.32993 14.36246  8.36563 15.84166
##  [533]  0.72769 10.26136  2.77336  5.74086 16.62536 17.67617 13.42003
##  [540] 14.79037 15.08022 19.25848  7.99470  6.12581 15.05301  6.50449
##  [547]  7.30715 18.74143 10.54840  9.07772  2.51386 14.96719 10.10381
##  [554] 18.18251 10.90451  2.54654  1.14210 13.32978 10.83622 18.57689
##  [561] 12.24161  3.69562  5.97455 18.97210 19.80190 12.75293 10.21117
##  [568] 13.24032  6.76077 16.80147 15.82719 16.20463  5.64417  2.79179
##  [575] 17.87445 15.50681  5.25500  2.81034 13.16426  6.39381  7.57468
##  [582] 11.37141 15.89481 11.59184 13.61938 13.24915 12.33301  5.19380
##  [589]  7.33782 15.57418 15.38092 19.64086  8.87015 10.46588  4.24575
##  [596]  0.42034 15.26499  6.69899  2.44955 14.75186  6.28877  5.93070
##  [603]  2.29145 18.16937 19.92037  8.83705  7.37170 10.87429 10.72219
##  [610]  6.31555 12.17229 14.51842 19.51827 10.72009 18.60979 16.74148
##  [617]  5.67641  7.83340 11.73502 17.39216 13.63519 15.18799 11.26205
##  [624] 14.94746 15.94757  2.15190  9.24835 17.68720  4.10570  0.88803
##  [631]  3.29576 18.18153 14.34457 12.43732  9.71434  3.12581 17.60986
##  [638]  0.02079  4.15501 19.78975 11.02894  1.61031 12.20375  0.09433
##  [645] 17.78218  1.56101 15.53399 19.18011 19.46718  9.00838  0.24892
##  [652] 11.31181 14.76086 19.32154 17.25638  5.94507 17.53781 16.16585
##  [659] 12.06543  9.33973  3.28631 10.01665 17.53579 13.73971  0.36371
##  [666] 13.89553  5.72148 10.00038 18.24201 17.83461  9.57575  3.93551
##  [673]  1.54033 14.95249  7.72040 14.76517  1.19327  3.11387 14.99927
##  [680]  7.76121  3.19215  3.17301 16.31710  3.73489 18.22575  1.52355
##  [687] 16.85532 11.36630  5.00854  1.29681  1.68358  1.82380 14.18518
##  [694]  3.35551 17.36570  7.44269 17.43688 10.13204 16.70377  1.51142
##  [701] 15.56300  2.90415 10.95338 14.18715 15.55158 16.43849  1.25548
##  [708]  4.50412  6.22163 13.26201  3.00103 13.57192 11.54853 19.72864
##  [715]  4.09891  0.62243 13.22012 10.20213 14.75118 14.43705 16.73823
##  [722] 12.65903 18.81118 17.55292  9.48805 17.24155  4.19531 14.20993
##  [729]  6.12277  7.45531 12.86946 13.04847 13.07963 14.14096 12.30234
##  [736]  7.69133 13.03307  9.56584 11.60283  2.65030  5.42330 11.44618
##  [743]  4.57268 10.57876 12.12021 16.95374 10.92151 18.54239 18.20001
##  [750]  0.64830 17.20106 19.52709 12.45394  0.35206 16.46854  0.36192
##  [757] 14.70009 12.90499 11.04291 10.30865 15.74185 17.84866 17.58852
##  [764]  8.05133 18.54571  2.48838 11.30530  6.20047  3.67366  0.04134
##  [771] 13.43828  1.47268  0.79248 16.61221  8.78355  7.32145 10.27682
##  [778]  9.39435 11.52595 18.85427 13.25606  5.74693  1.93661 12.43144
##  [785] 18.57090  8.19420  0.57549 11.47343 14.71401 11.46156  0.32010
##  [792]  5.82946  4.81556 15.26151 18.53318 14.83997 18.25781 14.50617
##  [799] 15.12141 15.52078  4.42294 12.66836  9.19959  4.69994  9.12471
##  [806]  3.97763 19.59804  9.97933 14.29724  0.71610 13.25904  7.11745
##  [813] 17.51443 17.24762 13.51386 12.44454  0.47260 13.49958  9.75073
##  [820]  7.42683  8.65003 11.08526 19.18698  8.84483  1.65224 10.00591
##  [827]  9.61175  4.69329 14.55127  0.55337  9.44609  4.85422 18.20729
##  [834]  6.84276 14.40390  5.50575 16.52617  3.95757 17.90088 10.32917
##  [841] 19.61473  3.59098  7.25606 19.36407  1.79920 14.46185  9.91310
##  [848] 12.37761  1.82189 10.31559  5.72389 10.10165 17.07006  3.18714
##  [855] 14.46657  5.71088  7.90640  1.01471  7.42780 17.89452  2.39723
##  [862]  8.81115 17.31036  3.48281 16.40197  5.97267  5.98219 18.08462
##  [869]  6.77677 17.68947 18.23951 14.67434 11.95454 15.42864 14.19417
##  [876]  2.30874 14.67383  2.55934 13.36030  7.43790 16.07117 15.75073
##  [883] 14.19254 17.81636 17.04495  7.46561  1.59403  7.35069 19.50349
##  [890] 12.90363 19.10262  0.56335  3.69655  4.20693 15.54631  6.10769
##  [897] 19.23404 16.02363 16.78136  7.01359 17.83289  2.54003  9.44482
##  [904]  7.64072 17.22315 17.50036  5.43466  2.87292 10.35664 19.32702
##  [911]  7.10969 12.27391 17.35716 16.71539  0.25949  6.50328  5.93168
##  [918] 19.58063  4.68273 10.19977 10.22220 19.91853  4.90112  7.29297
##  [925] 15.28484 12.98559  9.04583 15.16587 11.87278  2.16144 11.22689
##  [932]  4.32082  8.62701 11.03025 16.62890 10.14385  9.06765 18.65369
##  [939] 14.70041 10.40233  6.01408  1.20775 11.29110 19.49809 19.41840
##  [946]  2.50074  8.36486 18.19759  5.16907  9.55234  0.05196  9.47698
##  [953]  9.38137  8.28053  7.31173  3.59149  7.69443 16.99465  8.13605
##  [960]  5.33897  7.11739 19.34682  3.18275 12.55478  2.18667 18.28127
##  [967] 11.04165 18.28361  8.01848 17.47585 17.98221 16.47403  0.75165
##  [974]  3.65584 10.04567  9.16063  4.97160  2.25623  7.80682  3.16538
##  [981]  4.28163  7.20891 12.88825  7.21382  7.89136 14.80069 12.16573
##  [988] 17.36924  9.37420 11.91403 13.64926 11.52472  2.91803  1.98507
##  [995] 17.82809 18.47455  5.89921 13.73312 10.34570 16.89360
```

```r
## alternatively....
y <- x * 5
y
```

```
##  [1]  5 10 15 20 25 30 35 40 45 50
```


----

## Data structures
Vectors

- Vector Indexing: important, but only if you like using vectors. And R.
- In R, indexing begins at 1, not 0
- Can index a vector by name, if elements are named

```r
x[ c(1:5,8:10) ]         
[1] 1  2  3  4  5  8  9 10

x[ c(TRUE,FALSE) ]       ## recycling - common R feature. R will not give you a warning!
[1] 1 3 5 7 9            ## very useful, but make sure you are comparing vectors of same length

x > 5                    ## Boolean vector 
[1] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE

any(x > 5)              
[1] TRUE
all(x < 8)              
[1] FALSE
```

----

## Data structures
Vectors

- Vectorized Operations: Easiest way to acheive speed in R - apply a function to a vector

```r
f <- function (a,b) return(a^b)
f(x,2)          
```

- Even operators such as `+`, `-`, `*` are functions

```r
"*"(x,5)          ## returns 5 * x[1], 5 * x[2], ...
'['(x, x >5 )     ## returns vector with x[1] > 5, x[2] > 5, ..., x[10] > 5

                  ## if (condition) { do something } else { do something else }
ifelse(x < 5, x^2, 0)  
[1]  1  4  9 16  0  0  0  0  0  0
```

----

## Data structures
Vectors

- Vectorized Operations: More examples
- When coming from a different language, probably best NOT to translate verbatim
- Loops are your friend in C. In R, loops are like a bad friend - unrealiable at best.
- Under the hood, a vectorized operation is running a loop - in C. Much faster than in R.
- Vectorization also provides clarity (but don't get carried away one-lining everthing)

```r
logsum <- 0
x <- seq(100,10000,by=10)
for (i in 1:length(x)){
  logsum <- logsum + log(x[i])
}

# R translation
logsum <- sum(log(x))
```

----

## Data structures
Vectors

- Careful when thinking you are vectorizing
- Many R functions take a function as an argument
- `sum`, `max`, `min`, ... are exceptions

```r
mean(1,2,3)
[1] 1                 ## huh??

mean(c(1,2,3))
[1] 2                 ## that's better

max(1,2,3)
[1] 3
```

- Vectorization might not work when the current iteration depends on the previous
- Try to put code outside of loops when possible
- Use built-in functions such as rowSums(x) instead of apply(x,1,sum)...more later on this!

----

## Data structures
Vectors

- `NA` and `NULL`
- `NA` appears often in messy data, especially when a value doesn't exist
- R will attempt to calculate `NA`, and therefore return `NA`
- If R sees `NULL`, it skips it. `NULL` is non existant

```r
x <- c(5,10,NA,20,25)
mean(x)                 ## output is a numeric vector with NA as its value

is.na(x)                ## commonly used when cleaning data sets
[1] FALSE FALSE  TRUE FALSE FALSE
mean(x,na.rm=TRUE)      ## 15

x <- c(5,10,NULL,20,25)
mean(x)                 ## 15

length(NA)              ## NA is a logical constant of length 1
[1] 1
length(NULL)            ## NULL does not take any value. Undefined.
[1] 0
```

----

## Data structures
Vectors

- Filtering: Extremely useful for quick data analysis. Similar to indexing.


```r
x <- 1:10
x[x > 5]  ## What's happening here?
```

```
## [1]  6  7  8  9 10
```

- `x > 5` is a function call to `">"(a,b)` which returns `TRUE` or `FALSE` on every element of vector x. 
- Output of `x > 5` is boolean vector
- When used as an index on `x`...

----

## Data structures
Vectors

- Filtering


```r
x[c(FALSE, FALSE, FALSE, FALSE, FALSE, TRUE, TRUE, TRUE, TRUE, TRUE)]
```

```
## [1]  6  7  8  9 10
```

...returns elements of `x` that are `TRUE`

Common filtering functions include:
```r
subset(x, x > 5)      ## [1]  6  7  8  9 10
which(x > 5)          ## [1]  6  7  8  9 10
4%in%x                ## [1]  TRUE
```

----

## Data structures
Vectors

- Summary
- Everything in R is a vector
  - Filtering and indexing
  - `seq()`, `rep()`, `sample()`, `runif()`
  - `any()`, `all()`, `which()`, `subset()`
  - Recycling - R will not give you an error message

----

## Data structures
Matrices

- Matrices are vectors with two additional attributes: rows and columns
- Column-major order: insert values in first column, going down, then continuing to second column, going down, as so on


```r
x <- matrix(seq(1, 6, by = 1), nrow = 3, ncol = 2)  ## 3 by 2 matrix
x
```

```
##      [,1] [,2]
## [1,]    1    4
## [2,]    2    5
## [3,]    3    6
```

```r
x <- matrix(seq(1, 6, by = 1), nrow = 3, ncol = 3)  ## What's happening here??
```

```r
x <- matrix(seq(1,6,by=1),nrow=3)              ## same as above
x <- matrix(seq(1,6,by=1),nrow=3,byrow=TRUE)   ## row-major order    
```

----

## Data structures
Matrices

- Matrix operations

```r
x <- matrix(seq(1,4),nrow=2,ncol=2)
x + 5
x * 2
t(x)                        ## transpose
x %*% x                     ## cross product
x * x                       ## element-wise product
diag(x)                     ## diagonal components - identity matrix
det(x)                      ## determinant
eigen(x)                    ## list of eigenvalues and eigenvectors
```

- Remember your linear algebra!

----

## Data structures
Matrices

- Matrix indexing and filtering

```r
x[2,1]            ## second row, first column

x[,1]             ## all rows, first column. Vector form

x[,]              ## all rows, all columns. Same as print(x)

x[-1,]            ## remove first row. Negative indexing.
```

----

## Data structures
Matrices

- Matrix class

```r
x <- matrix( c(1:6), nrow=3, ncol=3)
class(x)                      ## matrix

y<-x[1,]                      ## 3 element vector
class(y)                      ## integer
attributes(y)                 ## returns NULL

y<-x[1,, drop=FALSE]     
class(y)                      ## matrix
attributes(y)                 ## 1 by 3 matrix

colnames(x) <- c( 'first col' , 'second col' , 'third col' )
rownames(x) <- c( 'row 1' , 'row 2' , 'row 3' )
```
- Higher dimension matrices also possible -> 'arrays'

----

## Data structures
Matrices

- Exercise!

```r
a) 
x <- matrix(rep(c(1,3,-1,2),5),ncol=4)
(i)  What is returned in the following?
     x[ x[1,] > 1,  c(1:2) ]
(ii) Find the column in x which has the largest sum. Hint - max(x) is your friend.

b) 
y <- matrix(c(c(1,2,4,8),c(2,3,-1,-7),c(0,5,12,-4),c(3,4,5,0)),ncol=4)
(i)  Calculate the trace of y (hint: trace of a matrix is the sum of the diagonals)
(ii) Replace the 3rd column with the sum of the first two columns

c)
Calculate the singular value decomposition of y. Do this the long and short way.
hint 1: SVD(A) = Q1*S*Q2, where Q1, Q2 contains the eigenvectors of A * t(A) and t(A) * A
hint 2: Access elements of a list using "____$vectors", i.e. x$vectors
```

----

## Data structures
Lists

- Combine objects of different types. Can have different `modes`.
- Forms basis for `data.frames`
- Vectors, matrices cannot be broken down into smaller components. Known as atomic vectors.
- Lists can be broken down - known as recursive vectors.

```r
x <- list(title='R presentation', date=format(as.POSIXlt(Sys.time(),"EDT"),"%m %d %Y")
          , num_attendees=10)
print(x)

$title
[1] "R presentation"
$date
[1] "10 28 2013"
$num_attendees
[1] 10
```

----

## Data structures
Lists

- Accessing `list` components


```r
## one bracket - [ - returns a list
class(x[1])
```

```
## [1] "numeric"
```


```r
## two brackets  -  [[  -  returns the actual element, in this case a character
x[[1]]
x$title
x[['title']]
```

----

## Data structures
Lists

- Accessing `list` components and values

```r
names(x)      
[1] "title"         "date"          "num_attendees"

unlist(x)       ## flattens the list into a vector

pres_1 <- format(as.POSIXlt(Sys.Date(),"EDT"),"%m %d %Y") 
pres_2 <- format(as.POSIXlt(Sys.Date()+30,"EDT"),"%m %d %Y") 

x <- list(title='R presentation', date=pres_1, num_attendees=10)
y <- list(title='2nd R presentation', date=pres_2, num_attendees=20)

list(x,y)       ## list of lists

unclass(x)      ## like unlist(x) but applied to any object. Usually returns a list
```

----

## Data structures
Lists

- The result of most statistical operations in R return a `list`
- Knowing how to manipulate lists is important

```r
n <- 100
x <- rnorm(n, mean = 0, sd = 1)          ## sample of 100 random normal variables (standard)
y <- 1 - 2 * x + rnorm(n)
f <- y ~ x                               ## y ~ x is a formula object
r <- lm(y ~ x)                           ## r is linear model object, i.e. linear regression
                                        
## the function str() - structure - is VERY useful in exploratory data analysis
## structure of r is a bunch of lists
str(r)

r$coeff
r$residuals
```

----

## Data structures
Data.frames

- The magic of R!
- Like a matrix of lists, of equal length
- Many R functions and packages assume input is in the form of a `data.frame`
- Allows for easy data manipulation
- Every CSV or Text file you read in is a `data.frame`, i.e. data in the real world is a `data.frame`

- Creating Data Frames


```r
z <- data.frame()
```


----

## Data structures
Data.frames


```r
y <- data.frame(col1 = c(1, 2), col2 = c("a", "b"), row.names = c("row1", "row2"))
y
```

```
##      col1 col2
## row1    1    a
## row2    2    b
```

```r
x <- data.frame(matrix(sample(c(50:100),size=12,replace=TRUE),nrow=6,ncol=2))

## return first column
x[,1]                 ## type depends on column values
x$X1                  ## type depends on column values
x[1]                  ## type data.frame
x['X1']               ## type data.frame
```

----

## Data structures
Data.frames

- Helpful `data.frame` functions

```r
x <- x[-6,]                   ## remove rows or columns with a "-" sign
y <- data.frame(names=c("dave","jenny","scott","mary","harry"))
z <- cbind(y,x)               ## column bind. Can be used on matrices too.
                              ## if you cbind two vectors you get a matrix, NOT data.frame

## alternatively you can create columns implicitly
x$names <- c("dave","jenny","scott","mary","harry")

w <- data.frame(names="megan",X1=82,X2=85)
z <- rbind(z,w)               ## row bind

## make sure number of elements in row, column are consistent
```

----

## Data structures
Data.frames

```r
## explicitly set names for z
names(z) <- c("names", "Exam 1","Exam 2")

## get dimensions
dim(z)                        
[1] 6 3

head(z)
tail(z)
```
- While very useful, `data.frames` are more memory intensive than matrices
- When initializing, if possible, preallocate `data.frame`
- Whenever possible, use matrices

----

## Data structures
Factors

- Used in many R packages and functions
- Comes from the notion of categorical variables in statistics
- Can be thought of as a `vector` with additional information - `levels`
- Used to split up data sets; commonly seen as columns of `data.frame`s


```r
x <- factor(c("finance", "tech", "tech", "auto", "finance", "energy", "tech"))
levels(x)
```

```
## [1] "auto"    "energy"  "finance" "tech"
```

```r
y <- factor(x, levels = c(levels(x), "tv"))  ## include new level, even though no tv data exists
```


---

## Data structures
Factors

- use `levels` to order your levels. Helpful when sorting factors


```r
wday <- c("mon", "tues", "mon", "wed", "fri", "wed")
wdayf <- factor(wday)
sort(wdayf)
```

```
## [1] fri  mon  mon  tues wed  wed 
## Levels: fri mon tues wed
```

```r
wdayf <- factor(wday, levels = c("mon", "tues", "wed", "thurs", "fri"))  ## let's add Friday as well
sort(wdayf)
```

```
## [1] mon  mon  tues wed  wed  fri 
## Levels: mon tues wed thurs fri
```


----

## Data structures
Factors

- Common `factor` functions

```r
z$names2 <- NULL                            ## NULL removes the object from the factor (or list)
z$gender <- c("m","f","m","f","m","f")
z$party <- c("D","D","R","R","D","D")

tbl <- table(z$gender,z$party)              ## contingency table. class "table"
addmargins(tbl)                             ## marginal sums
```

----

## Data structures
Factors

- Converting between factors and other types

```r
x <- seq(5,20,by=5)
f <- factor(x)
as.numeric(f)                    ## huh??
[1] 1 2 3 4

as.numeric(as.character(f))
[1]  5 10 15 20                  ## much better
as.numeric(levels(f))[f]         ## more efficient due to less conversions

## Is adding [f] necessary?
```

----

## Data structures
Summary

- `Vectors` - lifeblood of R
- `Matrices` - great for Math and Stats functions
- `Lists` - store complex objects
- `Data.frames` - the power of R
- `Factors` - good for statistics and categorization

----

## Control Structures

1. `for()`
2. `while()`
3. `repeat()`
4. `try()`
5. `if()`

----

## Control Structures
`for()`

```r
x <- seq(0,20,by=1) 

for (i in c(1:length(x))){
  x[i] <- x[i] * 2
}

## can be written on one line - but could make for messy code
for (i in c(1:length(x))) x[i] <- x[i] * 2
```
`while()`
```r
i=1
while (i < 22){
  x[i] <- x[i] * 2
  i <- i + 1
}
```

----

## Control Structures
`repeat()`

```r
x <- seq(0,20,by=1) 

i = 1
repeat {
  x[i] <- x[i] * 2
  i <- i + 1
  if (i > 21) break
}
```
`try()`
```r
try("hello" + 1, silent=FALSE)
try("hello" + 1, silent=TRUE)
tryCatch("hello" + 1, error = function(e) print("don't be ridiculous"))
```

----

## Control Structures
`if()`

```r
if (a == b) {
  # do something
} else {                  ## the else statement MUST be on the same line as the 
  # do something else     ## ending bracket of the if
}

if (a == b) do something

ifelse (a == b, x, y)     ## use ifelse() on vectors
```

----

## Control Structures

- Exercise!

```r
(a) Write a loop to scan through an integer vector to determine the index of the 
maximum value. The loop should terminate as soon as the index is obtained. Ignore ties.

(b) Redo the above using built-in R functions such as rank(), sort() and order()
```

----

## Functions

1. Functions
2. Arguments
3. Environment
4. Pointers
5. Generic

----

## Functions
Functions

- Write functions - it's good practice
- each function should perform a specified task - easily understood inputs and outputs
- function() is a built-in R function whose job is to create functions...#mindblown

```r
power <- function(x,y){
  return(x^y)
}

power(2,4)
[1] 16
```

- The right hand side of power() has two arguments: the parameters and the body
- To get the code of a function, you can just type its name -- with no brackets.

----

## Functions
Arguments

```r
formals(power)        # $x   $y   These are the arguments to power
body(power)           # { return (x^y) }
power                 # prints out the entire function - good if you forget what's in it!
```
- try it out on any built-in R function to see its innards
- Note that it won't work on some functions that are written in C (e.g  sum, mean)

----

## Functions
Arguments

- Arguments can have default values.

```r
f <- function(x, y=3) { ... }

## Some functions have tons of parameters. You don't need to enter them all.
f <- function(x, ...) {
  plot(x, ...)
}
```
- Anonymous functions. Single use. No name. No feelings exchanged.
```r
apply (x, 2, function(x) sum[x>2])
```

----

## Functions
Environment and Scope

- A function consists of its arguments, body and environment

```r
d <- 8
f <- function(y){
  x <- 3 * y
  h <- function (x,d){
    return(y*(x+d))
  }
  return(x+h(x,d))
}
f(2)

# d is global to f()
# x is local to f() and global to h()
# h cannot be called at the "top level" since it's environment is limited to f()'s
```

----

## Functions
Environment and scope

- Mini Exercise!

```r
Write a function that finds the maximum value in corresponding indices for two vectors.

e.g. 
x <- c(1,2,3,4)
y <- c(0,3,5,4)
## output should be 
[1] 1 3 5 4
```

----

## Functions
Environment and scope

```r
ls()           # returns all the variables in the environment
               # good to know when you've created a ton and are starting to lose track
rm(x)          # rm(x) deletes x...rm(list=ls()) is usually not a great idea!

f <- function (x){
  x <<- 2      # declare a global variable within a function. Usually not good practice.
  return(x)
}
x<-1
f(x)

# You can even make custom operators!
"%powerUp%" <- function(a,b) return (a^b)

3%powerUp%2                                 
[1] 9
```

----

## Functions
Pointers

- R does not have pointer variables like Python

```r
# in Python
>>> x <- c(5,2,8)
>>> x.sort()             ## this doesn't exist in R
>>> x
[2, 5 , 8]

# in R
x <- c(5,2,8)
sort(x)
[1] 2 5 8
x
[1] 5 2 8
x <- sort(x)
x
[1] 2 5 8
```

----

## Functions
Generic functions

- R is a dialect of S3 (S4 is the latest)
- S3 has generic functions, such as `print()`, `plot()`, `summary()`

```r
data(cars)
fit <- lm(dist~speed,data=cars)
summary(fit)

## different output from the same function!
summary(c(1,2,3))

## lists out all the methods for the summary function
methods(summary)  
```

- there is a `summary.lm()` function and a `summary.default()` function
- makes it harder to get the object that is printed, but this is possible

----

## Functions
Generic functions

- Exercise!

```r
a) Get the Adjusted R-squared from the regression of distance on speed example
b) Get the t-value of the X variable (i.e. speed)
c) Predict the braking distance if going 200 miles per hour.
```

----

## Commonly used built-in functions

1. `apply()` 
2. `lapply()`, `tapply()`, `sapply()`
3. `mapply()`
4. `by()`, `cut()`, `aggregate()`, `split()`

----

## Commonly used built-in functions
`apply()`

- Apply a function to a row or column of a matrix

```r
x <- matrix(sample(c(0:100),20,replace=TRUE),nrow=5,ncol=4)
apply(x,1,sum)                                   ## sum rows
apply(x,1,function(x) x^2)                       ## apply function to every element
                                                 ## What type of function is this?
```

- Easy to read
- Less lines of code
- NOT faster than for loops. Loops are built into these functions.

----

## Commonly used built-in functions
`lapply()`, `tapply()`, `sapply()`

- like `apply()` for other data structures

```r
lapply(list(z$'Exam 1',z$'Exam 2'),mean)    ## mean of Exam scores; returns a list
                                            ## like apply() but can be used on data.frames
sapply(list(z$'Exam 1',z$'Exam 2'),mean)    ## mean of Exam scores; returns a vector
sapply(list(z$'Exam 1',z$'Exam 2'),mean,simplify=FALSE)   ## same as lappy()

## find mean exam 1 scores, split by party
tapply(z$'Exam 1',z$party,FUN = mean,simplify=TRUE)      ## simplify determines output type
```

----

## Commonly used built-in functions
`mapply()`

- apply a function to corresponding elements of a list
- simplify determines output type - defaults to TRUE

```r
a<-c(1:5);b<-c(6:10);d<-c(11:15);
mapply(sum,a,b,d)
sum(a[1],b[1],d[1])
sum(a[2],b[2],d[2])

mapply(mean,a,b,d)            ## What's happening here?
```

----

## Commonly used built-in functions
`by()`, `cut()`, `aggregate()`, `split()`

- Like `apply()`, but used on `data.frames`
- Split, apply, combine
- Package `plyr` is very popular and useful, but important to learn Base R first.

```r
aggregate(z[,c(2:3)],by=list(z$party),mean)          ## mean Exam score by party
aggregate(z[,c(2:3)],by=list(z$part, z$gender),sum)  ## sum by party and gender

## same as tapply() but for data.frames (instead of arrays)
## returns class "by"
by(z$'Exam 1',z$party,sum)

## convert numeric column of data.frame into factor
## great for binning data
cut()

split(z,f = z$gender)                       ## split a dataframe according to a factor
```

----

## Commonly used built-in functions
Exercise!

```r
a)  
Find the average grade for each student.
    D is between 50 and 59. C is between 60 and 69. B is between 70 and 79. 
    A is between 80 and 100.

b)  
Execute the equivalent of the following SQL code, in but in R:
      SELECT nature, SUM(amount)
      FROM expenses
      GROUP BY nature
c)
(i)   The function system.time() returns timings for R operations. Examine the help documentation about this function. 
(ii)  Compute the median standard deviation of every column of a 100 by 100 matrix. Initialize a 100 x 100 matrix using a Random Uniform Variable, between 20 and 50 in each cell. Compute the median standard deviation of each column using:
  (1) A for-loop
  (2) An apply function
(iii) Which is the fastest?
```

----

## String Manipulation
Basic string functions

```r
example <- c("THIS IS AN EXAMPLE","and so is this","this is not","hello world","extra")
grep("an",example)            
[1] 2
grep("an",example,ignore.case=TRUE)
[1] 1 2
grep("an",example,ignore.case=TRUE,value=TRUE)
[1] "THIS IS AN EXAMPLE" "and so is this" 

nchar(example)
[1] 18 14 11 11  5

paste(example[1],example[2])
[1] "THIS IS AN EXAMPLE and so is this"
files <- c("ex1","ex2")
for (i in files){
   ggsave(filename = paste("Title",i,".pdf"))
}
```

----

## String Manipulation
Basic string functions

```r
# formatting strings
sprintf("%f",exp(1))
[1] "2.718282"
sprintf("%0.2f",exp(1))
[1] "2.72"
sprintf("Today's date is %s",format(Sys.Date(),"%d %b %Y"))
[1] "Today's date is 31 Oct 2013"

example2 <- "Substring takes a sub-set of...the string!...It's nuts!"
paste(substr(example2,19,21),substr(example2,23,25),sep='')
[1] "subset"
```

----

## String Manipulation
Basic string functions

```r
sp <- strsplit(example2,split="of")
sp
[[1]]
[1] "Substring takes a sub-set "  "...the string!...It's nuts!"

length(sp)
[1] 1

length(unlist(sp))
[1] 2

regexpr("!",example2)     ## first occurence of "!" in example2

gregexpr("!",example2)    ## all occurrences of "!" in example2
```

----

## String Manipulation
Exercise!

```r
a) Convert the following character vector into a 3 column dataframe. Name each column.
b) Format the numbers to be percentages with 2 decimal places.
c) Find the total score for people with J-letter first names. 

char_vec <- c("{'al' 'einst'} score:0.4503-[12302013]",
"{'isaac' 'knewt'} score:0.0007-[11202013]",
"{'ralph' 'emerson'} score:0.10321-[09122013]",
"{'james' 'dean'} score:0.84-[02032012]",
"{'jim' 'beam'} score:0.2-[10172013]",
"{'tommy' 'bahamas'} score:0.761-[05212013]",
"{'george' 'of the jungle'} score:0.9434-[01302013]",
"{'harry' 'henderson'} score:0.5456-[08112012]",
"{'johnny' 'walker'} score:0.309118-[08212011]")

d) Print out the following sentence with one word on each line:
y <- "This is a sentence."
```

----

## Miscellaneous Tips and tricks

- Basic statistical functions
- `mean(x)`, `median(x)`, `sd(x)`, `var(x)`, `cov(x,y)`, `cor(x,y)`

```r
x <- rnorm(1000,85,5)
y <- 2 * runif(1000,0,10)
mean(x)             ## [1] 85.22434
median(x)           ## [1] 85.24506
sd(x)               ## [1] 4.869123
var(x)              ## [1] 23.70836
sd(y)               ## [1] 5.736198
cov(x,y)            ## [1] 0.8053751
cor(x,y)            ## [1] 0.02883522
``` 

----

## Miscellaneous Tips and tricks

- Be mindful of operator precendence

```r
1:n-1       ## wrong
1:(n-1)     ## this is what you want
```

```r
-2.4 ^ 2.5  ## nice    
[1] -8.923354
x <- -2.4
x ^ 2.5     ## not so nice
[1] NaN
```

- Parenthesis will force the operator to do what you want

----

## Miscellaneous Tips and tricks

- Boolean operations coerce numbers to being `TRUE`

```r
x == 4 | 6          ## OR function - returns bogus result
x == 4 | TRUE       ## weird

x == 4 | x == 6     ## better

x %in% c(4,6)       ## best
```

----

## Miscellaneous Tips and tricks

- coercion - sometimes it's good to coerce
- `read.csv()` returns a `data.frame`. What if you want to do math? 

```r
x <- data.frame(num=c(1,2,3,4))
mean(x)                             ## Nope
x <- as.matrix(x)
mean(x)                             ## Yup

as.numeric()
as.character()
as.factor()
as.data.frame()
```

----

## Miscellaneous Tips and tricks
`print()` vs `cat()`

- `print()` is a generic function
- `cat()` is a concatenate function

```r
x <- 2
print("One plus one is",x)
[1] "One plus one is"
## alternatively...
print("One plus one is");print(x);
[1] "One plus one is"
[1] 2
## even better...
cat(paste("One plus one is",x))
One plus one is 2
```

----

## Miscellaneous Tips and tricks
`class` vs `mode`

- An object's `mode` determines how it's stored in memory 
- An objects `class` determines its abstract type, a concept borrowed from OOP.


```r
x <- data.frame(scores = c(80, 90, 70))
y <- as.Date("2013-11-05")
cat(paste(mode(x), mode(y)))
```

```
## list numeric
```

```r
cat(paste(class(x), class(y)))
```

```
## data.frame Date
```


----

## Miscellaneous Tips and tricks
`do.call()`

- lots of real data comes in row form, each element is a different `mode`
- many times stored as a list. Use `do.call` to combine the elements into a `data.frame`


```r
a <- list(1.3, 2.5, "jeff")
b <- list(4.5, 2.8, "jerry")
d <- list(6.5, 0.8, "joe")
z <- list(a, b, d)
df <- data.frame(do.call(rbind, z))
df
```

```
##    X1  X2    X3
## 1 1.3 2.5  jeff
## 2 4.5 2.8 jerry
## 3 6.5 0.8   joe
```


----

## Miscellaneous Tips and tricks

- Mini Exercise!

```r
a)
## Create a new column called num2 for which each value is double the corresponding value in num
## Make sure num2 is also a factor
x <- data.frame(num=factor(c(1.0,0.03,8.0, 0.4)))

b)
## Find the letters in z corresponding to the indices of even numbers in y
y <- c(1,2,NA,4,5,8,5,2)
z <- c("f","g","e","i","l","o","p","u")
```

----

## Not covered

1. Object oriented programming with S3 and S4 
2. Input/output
3. Packages: `ggplot`, `reshape`, `plyr`, `forecast`, `MASS`
4. Debugging: `browser()`, `warnings()`
5. Parallelizing
6. Much more

----

## Resources

1. The Art of R Programming
2. R cookbook
3. Computing for Data Analysis (Coursera)

----

## Questions?

----
