Red Wine Quality by Mario Farina
========================================================



# Objective

The objective of this project is to explore the relationship between the quality of wines (as assessed by experts) and 11 of their chemical properties.

# About the data set
This is tidy data set with 1,599 red wines. For each one of them the data set includes 11 variables based on physicochemical tests and "quality" variable that originates from the rating of at least 3 wine experts who provided a rating between 0 and 10.
More information can be found here:
https://s3.amazonaws.com/udacity-hosted-downloads/ud651/wineQualityInfo.txt





# Quick look at the data
First, I run some basic functions to get an idea of what's in the data and what is the structure of the file.


```
## [1] 1599   13
```

```
##  [1] "X"                    "fixed.acidity"        "volatile.acidity"    
##  [4] "citric.acid"          "residual.sugar"       "chlorides"           
##  [7] "free.sulfur.dioxide"  "total.sulfur.dioxide" "density"             
## [10] "pH"                   "sulphates"            "alcohol"             
## [13] "quality"
```

There are 13 variables instead of the 11 + quality as described in the info file. The "X" variable is just an index or unique id. "id" would have been a better name so I rename it. It will be completely ignored from now on anyway.



Output some basic information about the data.


```
##        id         fixed.acidity   volatile.acidity  citric.acid   
##  Min.   :   1.0   Min.   : 4.60   Min.   :0.1200   Min.   :0.000  
##  1st Qu.: 400.5   1st Qu.: 7.10   1st Qu.:0.3900   1st Qu.:0.090  
##  Median : 800.0   Median : 7.90   Median :0.5200   Median :0.260  
##  Mean   : 800.0   Mean   : 8.32   Mean   :0.5278   Mean   :0.271  
##  3rd Qu.:1199.5   3rd Qu.: 9.20   3rd Qu.:0.6400   3rd Qu.:0.420  
##  Max.   :1599.0   Max.   :15.90   Max.   :1.5800   Max.   :1.000  
##  residual.sugar     chlorides       free.sulfur.dioxide
##  Min.   : 0.900   Min.   :0.01200   Min.   : 1.00      
##  1st Qu.: 1.900   1st Qu.:0.07000   1st Qu.: 7.00      
##  Median : 2.200   Median :0.07900   Median :14.00      
##  Mean   : 2.539   Mean   :0.08747   Mean   :15.87      
##  3rd Qu.: 2.600   3rd Qu.:0.09000   3rd Qu.:21.00      
##  Max.   :15.500   Max.   :0.61100   Max.   :72.00      
##  total.sulfur.dioxide    density             pH          sulphates     
##  Min.   :  6.00       Min.   :0.9901   Min.   :2.740   Min.   :0.3300  
##  1st Qu.: 22.00       1st Qu.:0.9956   1st Qu.:3.210   1st Qu.:0.5500  
##  Median : 38.00       Median :0.9968   Median :3.310   Median :0.6200  
##  Mean   : 46.47       Mean   :0.9967   Mean   :3.311   Mean   :0.6581  
##  3rd Qu.: 62.00       3rd Qu.:0.9978   3rd Qu.:3.400   3rd Qu.:0.7300  
##  Max.   :289.00       Max.   :1.0037   Max.   :4.010   Max.   :2.0000  
##     alcohol         quality     
##  Min.   : 8.40   Min.   :3.000  
##  1st Qu.: 9.50   1st Qu.:5.000  
##  Median :10.20   Median :6.000  
##  Mean   :10.42   Mean   :5.636  
##  3rd Qu.:11.10   3rd Qu.:6.000  
##  Max.   :14.90   Max.   :8.000
```

```
## 'data.frame':	1599 obs. of  13 variables:
##  $ id                  : int  1 2 3 4 5 6 7 8 9 10 ...
##  $ fixed.acidity       : num  7.4 7.8 7.8 11.2 7.4 7.4 7.9 7.3 7.8 7.5 ...
##  $ volatile.acidity    : num  0.7 0.88 0.76 0.28 0.7 0.66 0.6 0.65 0.58 0.5 ...
##  $ citric.acid         : num  0 0 0.04 0.56 0 0 0.06 0 0.02 0.36 ...
##  $ residual.sugar      : num  1.9 2.6 2.3 1.9 1.9 1.8 1.6 1.2 2 6.1 ...
##  $ chlorides           : num  0.076 0.098 0.092 0.075 0.076 0.075 0.069 0.065 0.073 0.071 ...
##  $ free.sulfur.dioxide : num  11 25 15 17 11 13 15 15 9 17 ...
##  $ total.sulfur.dioxide: num  34 67 54 60 34 40 59 21 18 102 ...
##  $ density             : num  0.998 0.997 0.997 0.998 0.998 ...
##  $ pH                  : num  3.51 3.2 3.26 3.16 3.51 3.51 3.3 3.39 3.36 3.35 ...
##  $ sulphates           : num  0.56 0.68 0.65 0.58 0.56 0.56 0.46 0.47 0.57 0.8 ...
##  $ alcohol             : num  9.4 9.8 9.8 9.8 9.4 9.4 9.4 10 9.5 10.5 ...
##  $ quality             : int  5 5 5 6 5 5 5 7 7 5 ...
```

The most important things to notice about the data at this stage are:

- All variables are numeric
- All variables except quantity are continuous variables and coded as numerics
- quality is an ordinal variable and coded as an integer
- quality ranges from 3 to 8, has a median of 6 and a mean of 5.636

# Univariate Analysis Section
First, I create 2 sets of histogram plots, each containing a histogram for all the 12 variables. The first set with standard histograms and the second with a logarithmic scale of 10.

### Histograms

![plot of chunk Univariate_Plots](Figs/Univariate_Plots-1.png)
### Histograms log10 scale

![plot of chunk Univariate_Plots_log10](Figs/Univariate_Plots_log10-1.png)

I notice that some are normally distributed and some are positively skewed. At first look, citric acid seems to have a bimodal distribution.

However, when plotted on a base 10 logarithmic scale all distribusions tend to become more normal.

### Quality

The most important variable to investigate at this stage however is quality so I look at its distribution separately.


```
## 
##   3   4   5   6   7   8 
##  10  53 681 638 199  18
```

Histograms:

![plot of chunk unnamed-chunk-5](Figs/unnamed-chunk-5-1.png)

![plot of chunk unnamed-chunk-6](Figs/unnamed-chunk-6-1.png)

The histograms show that the values are normally distributed. Based on this visualization it appears that most wines in the sample are average (grade 5 and 6), some are bad (3 and 4) and some are good (7 and 8). 
Based on this distinction, I create a categorical "grade" variable for quality, where the values are (1) bad, (2) average and (3) good.



Show counts.


```
##     bad average    good 
##      63    1319     217
```

### Citric acid

Citric acid is the variable with the most unusual distribution.
Changing the number of bins to 10 produces a fairly rectangular shape, with the counts dropping after 0.5 and few outliers close to 1.

![plot of chunk unnamed-chunk-9](Figs/unnamed-chunk-9-1.png)

![plot of chunk unnamed-chunk-10](Figs/unnamed-chunk-10-1.png)

The histogram produced using a logarithmic scale of 10 looks very different because of the 0 values.
This is the only variable with 0 values, which I thought is worth investigating.


```
## [1] 132
```

I am going to accept the 132 zero values as genuine for two reasons:
- 1. The documentation on the data set states that there aren't any attributes with missing values.
- 2. A quick Google search revealed that there are indeed wines without citric acid (see references).

# Bivariate Analysis

First, in order to focus the analysis on the most interesting variables I want to find out which variables have the highest level of correlation with quality.


```
## [1] "fixed acidity: 0.124051649113224"
```

```
## [1] "volatile acidity: -0.390557780264007"
```

```
## [1] "citric acid: 0.226372514318041"
```

```
## [1] "residual sugar: 0.0137316373400663"
```

```
## [1] "chlorides: -0.128906559930053"
```

```
## [1] "free sulfur: -0.0506560572442764"
```

```
## [1] "total sulfur dioxide: -0.185100288926538"
```

```
## [1] "density: -0.174919227783349"
```

```
## [1] "pH: -0.0577313912053821"
```

```
## [1] "sulphates: 0.251397079069261"
```

```
## [1] "alcohol: 0.476166324001136"
```


![plot of chunk unnamed-chunk-12](Figs/unnamed-chunk-12-1.png)

The 4 attributes that are most highly correlated to quality are:

- alcohol
- volatile acidity
- sulphates
- citric acid

I am going to focus on these 4 so I create a new data frame with only the variables in which I am interested, to reduce processing time.



Using the small data frame with the subset of variables of interest I create a scatterplot matrix.

![plot of chunk unnamed-chunk-14](Figs/unnamed-chunk-14-1.png)

What I notice immediately is that alcohol is positively correlated to quality, and citric acid is negatively correlated to volatile acidity, which is the strongest relationship visible here.

I want to look at the relationship between quality and alcohol more in depth since that seems to be the most relevant finding to answer the research question.

![plot of chunk unnamed-chunk-15](Figs/unnamed-chunk-15-1.png)

The three plots side by side clearly show how wines of higher quality tend to have more alcohol, although wines graded 5 have less alcohol than wines graded 3, so the relationship is not perfectly linear.

Another way to explore this relationship is to look at the averages for each quality grade.


```
##   quality   alcohol
## 1       3  9.955000
## 2       4 10.265094
## 3       5  9.899706
## 4       6 10.629519
## 5       7 11.465913
## 6       8 12.094444
```

```
##     grade  alcohol
## 1     bad 10.21587
## 2 average 10.25272
## 3    good 11.51805
```

```
## df_small$quality: 3
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   8.400   9.725   9.925   9.955  10.580  11.000 
## -------------------------------------------------------- 
## df_small$quality: 4
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    9.00    9.60   10.00   10.27   11.00   13.10 
## -------------------------------------------------------- 
## df_small$quality: 5
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##     8.5     9.4     9.7     9.9    10.2    14.9 
## -------------------------------------------------------- 
## df_small$quality: 6
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    8.40    9.80   10.50   10.63   11.30   14.00 
## -------------------------------------------------------- 
## df_small$quality: 7
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    9.20   10.80   11.50   11.47   12.10   14.00 
## -------------------------------------------------------- 
## df_small$quality: 8
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    9.80   11.32   12.15   12.09   12.88   14.00
```

Looking at the averages shows that the difference in level of alcohol is very small between "bad" and "average" wine, but quite significant between "average" and "good".

It's also worth pointing out that the lowest level of alcohol among the wines with the highest quality (9.8) is lower than the highest level of alcohol among the wines with the lowest quality (11), so a high level of alcohol is neither sufficient nor necessary for quality.

# Multivariate Analysis

I am going to explore the other variables of interest (volatile acidity, sulphates and citric acid) splitting the data by quality grade using facet_wrap (because quality is the main variable under investigation) and always visualising the level of alcohol through size (because it's the most highly correlated to quality).

Excluding quality and alcohol, the strongest relationships I have seen are between:

- 1. citric acid and volatile acidity
- 2. sulphates and volatile acidity
- 3. sulphates and citric acid

![plot of chunk Multivariate_Plots](Figs/Multivariate_Plots-1.png)![plot of chunk Multivariate_Plots](Figs/Multivariate_Plots-2.png)![plot of chunk Multivariate_Plots](Figs/Multivariate_Plots-3.png)

In all three plots the dots are larger and warmer in the "good" section because of the correlation between wine quality and alcohol, which was already discovered.

The relationship between citric acid and volatile acidity is strong and is somewhat different in the three quality grade sections. Looking at the "bad" wines, the dots are mostly on the left (low citric acid) and middle of y axis (volatile acidity), with some outliers on the top. The shape is similar for the average wines, but without extreme outliers. A clear difference can be noticed in the "good" section, where the concentration of dots increases in the middle of the x axis and bottom of the y axis because volatile acidity is negatively correlated to quality and citric acid is positively correlated.

In the case of sulphates is interesting to notice how good wines have more than bad wines but at the same time without extremely high values, which instead are visible in bad and average wines.

Looking at the relationship between quality and the three variables examined here, a correlation also seems evident looking at the box plots.

### Box plots
![plot of chunk box_plots](Figs/box_plots-1.png)

# Final Plots and Summary

### Plot One
![plot of chunk Plot_One](Figs/Plot_One-1.png)

### Description One
This is the same plot as the one in the "Quality" section, but simplified showing only 3 bins.
Wine quality is normally distributed in the dataset, with average wines (scores 5 to 6) being the vast majority.

### Plot Two
![plot of chunk Plot_Two](Figs/Plot_Two-1.png)

### Description Two
There is a fairly linear correlation between quality and alcohol, although this is not true if only wines in the bottom half of the quality scale are considered. Also, outliers in the average section show that an increase in alcohol does not alone determine an increase in quality.

### Plot Three
![plot of chunk Plot_Three](Figs/Plot_Three-1.png)

### Description Three
The other three variables with the highest correlation to quality are, in order, volatile acidity, sulphates and citric acid. It's very evident from the box plots how the first is negatively correlated to quality while the other two are positively correlated. Although this is less the case for citric acid, all variables show outliers, sometimes in both directions, so none of them could be used to reliably predict alone the quality of the wine.


# Reflection
Before drawing any conclusion from the data, there are two important considerations to be made about the data set. First, the sample size of the "good" wines (28) is very limited and second, the quality of the wines has been assessed by a limited number of experts. The documentation also states that the quality was assessed by "at least 3 evaluations", which suggests that different wines may have been graded by different experts and in different numbers, which means not all wines have been graded with a consistent method. This would be a particularly serious problem if, for example, some wine experts prefer wines with a high alcohol concentration more than others. If the data included IDs for the expert who contributed in assessing the quality of the wines this could have been investigated. Another issue with the subjective nature of the quality measurement is that some experts may tend to rate wines as good or bad instead of average more or less easily, which affects the distribution and the standard deviation of the quality variable.

In short I see a real issue with the operational definition of quality in this data set and with the level of information provided in the documentation available.

Having said that, there are some general findings that could be made about the direction, and to an extent magnitude, of the correlation between quality and certain variables.

# References
Citric acid in red wine:
https://en.wikipedia.org/wiki/Acids_in_wine#Citric_acid
http://www.livestrong.com/article/189520-what-drinks-do-not-contain-citric-acid/

Renaming fields:
http://stackoverflow.com/questions/7531868/how-to-rename-a-single-column-in-a-data-frame-in-r

Creation of categorical variables:
http://stackoverflow.com/questions/22075592/creating-category-variables-from-numerical-variable-in-r

http://www.r-bloggers.com/from-continuous-to-categorical/

Plot with percentages:
http://stackoverflow.com/questions/9317948/how-to-label-histogram-bars-with-data-values-or-percents-in-r

Simple correlation
http://www.r-tutor.com/elementary-statistics/numerical-measures/correlation-coefficient
http://www.gardenersown.co.uk/education/lectures/r/correl.htm
http://www.statmethods.net/stats/correlations.html

Concatenating strings
http://stackoverflow.com/questions/7201341/how-can-2-strings-be-concatenated-in-r

Sorting data frames
http://stackoverflow.com/questions/1296646/how-to-sort-a-dataframe-by-columns

Bar charts
http://www.cookbook-r.com/Graphs/Bar_and_line_graphs_(ggplot2)/

Drop columns
http://stackoverflow.com/questions/4605206/drop-data-frame-columns-by-name

GGpairs
https://rpubs.com/fraki22/122149

Density plots:
http://docs.ggplot2.org/current/geom_density.html

Aggregate function:
https://learningstatisticswithr.wordpress.com/2012/11/28/a-simple-way-to-calculate-group-means-in-r/

facet_wrap:
http://docs.ggplot2.org/0.9.3.1/facet_wrap.html

scale_colour_gradient2:
http://docs.ggplot2.org/0.9.3.1/scale_gradient2.html

Plotting average values for levels:
http://stackoverflow.com/questions/11857935/plotting-the-average-values-for-each-level-in-ggplot2


```
## Error in parse_block(g[-1], g[1], params.src): duplicate label 'global_options'
```

```
## Error in readLines(con): cannot open the connection
```
