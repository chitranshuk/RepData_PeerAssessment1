# Reproducible Research: Peer Assessment 1
## Settings
echo = TRUE

## Loading and preprocessing the data

Below are the steps for loading the data for Initial Analysis.
Loaded the file and removed the row with missing values in the original data File

```r
DataFile <- read.csv("activity.csv",sep=",",colClasses = c("numeric","Date","numeric"))
FinalFile <- na.omit(DataFile)
summary(DataFile)
```

```
##      steps             date               interval     
##  Min.   :  0.00   Min.   :2012-10-01   Min.   :   0.0  
##  1st Qu.:  0.00   1st Qu.:2012-10-16   1st Qu.: 588.8  
##  Median :  0.00   Median :2012-10-31   Median :1177.5  
##  Mean   : 37.38   Mean   :2012-10-31   Mean   :1177.5  
##  3rd Qu.: 12.00   3rd Qu.:2012-11-15   3rd Qu.:1766.2  
##  Max.   :806.00   Max.   :2012-11-30   Max.   :2355.0  
##  NA's   :2304
```

```r
summary(FinalFile)
```

```
##      steps             date               interval     
##  Min.   :  0.00   Min.   :2012-10-02   Min.   :   0.0  
##  1st Qu.:  0.00   1st Qu.:2012-10-16   1st Qu.: 588.8  
##  Median :  0.00   Median :2012-10-29   Median :1177.5  
##  Mean   : 37.38   Mean   :2012-10-30   Mean   :1177.5  
##  3rd Qu.: 12.00   3rd Qu.:2012-11-16   3rd Qu.:1766.2  
##  Max.   :806.00   Max.   :2012-11-29   Max.   :2355.0
```

```r
head(FinalFile)
```

```
##     steps       date interval
## 289     0 2012-10-02        0
## 290     0 2012-10-02        5
## 291     0 2012-10-02       10
## 292     0 2012-10-02       15
## 293     0 2012-10-02       20
## 294     0 2012-10-02       25
```

## What is mean total number of steps taken per day?

1. Make a histogram of the total number of steps taken each day

For above the aggregate function is used to sum the total number of steps each day which is displayed in the histogram



```r
WorkFile <- aggregate(FinalFile$steps,list(Date = FinalFile$date),FUN=sum)
names(WorkFile) <- c("Date","Total_Steps")
head(WorkFile)
```

```
##         Date Total_Steps
## 1 2012-10-02         126
## 2 2012-10-03       11352
## 3 2012-10-04       12116
## 4 2012-10-05       13294
## 5 2012-10-06       15420
## 6 2012-10-07       11015
```

```r
hist(WorkFile$Total_Steps,main="Histogram of Total Steps", breaks= 10,xlab="Daily - Total Number of Steps",col="blue")
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png) 

2. Calculate and report the mean and median total number of steps taken per day


```r
WorkFileMean <- mean(WorkFile$Total_Steps)
WorkFileMedian <- median(WorkFile$Total_Steps)
```

1. Mean of the the total number of Step per day = 1.0766189\times 10^{4}
2. Median of the the total number of Step per day = 1.0765\times 10^{4}

## What is the average daily activity pattern?

1. Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis)
and the average number of steps taken, averaged across all days (y-axis)



```r
WorkFile <- aggregate(FinalFile$steps,list(Interval=FinalFile$interval),FUN=mean)
names(WorkFile) <- c("Interval","Average")
plot(WorkFile$Interval,WorkFile$Average,type="l",col="red",xlab="5-Minute Interval Time",ylab="Average Number of Steps")
```

![](PA1_template_files/figure-html/unnamed-chunk-4-1.png) 

2. Which 5-minute interval, on average across all the days in the dataset,
contains the maximum number of steps?


```r
RowValue <- which.max(WorkFile$Average)
MaxInterval <- WorkFile[RowValue,]
MaxValue <- MaxInterval$Interval
```

The Time Interval 835 has the maximum steps taken on an average

## Imputing missing values




## Are there differences in activity patterns between weekdays and weekends?
