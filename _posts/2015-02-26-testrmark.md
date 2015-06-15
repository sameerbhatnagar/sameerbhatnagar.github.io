---
title: "Testing RMarkdown"
author: "sahir"
date: '2015-02-26'
layout: post
tags:
- R
- regression
comments: yes 
---

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.
 
When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:


{% highlight r %}
summary(cars)
{% endhighlight %}



{% highlight text %}
##      speed           dist       
##  Min.   : 4.0   Min.   :  2.00  
##  1st Qu.:12.0   1st Qu.: 26.00  
##  Median :15.0   Median : 36.00  
##  Mean   :15.4   Mean   : 42.98  
##  3rd Qu.:19.0   3rd Qu.: 56.00  
##  Max.   :25.0   Max.   :120.00
{% endhighlight %}

<!--more-->

You can also embed plots, for example:

![plot of chunk cars](/figure/posts/2015-02-26-testrmark/cars-1.png) 

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.


{% highlight r %}
summary(fit<-lm(speed~dist, cars))
{% endhighlight %}



{% highlight text %}
## 
## Call:
## lm(formula = speed ~ dist, data = cars)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -7.5293 -2.1550  0.3615  2.4377  6.4179 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  8.28391    0.87438   9.474 1.44e-12 ***
## dist         0.16557    0.01749   9.464 1.49e-12 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 3.156 on 48 degrees of freedom
## Multiple R-squared:  0.6511,	Adjusted R-squared:  0.6438 
## F-statistic: 89.57 on 1 and 48 DF,  p-value: 1.49e-12
{% endhighlight %}


{% highlight r %}
plot(fit)   
{% endhighlight %}

![plot of chunk lmplot](/figure/posts/2015-02-26-testrmark/lmplot-1.png) ![plot of chunk lmplot](/figure/posts/2015-02-26-testrmark/lmplot-2.png) ![plot of chunk lmplot](/figure/posts/2015-02-26-testrmark/lmplot-3.png) ![plot of chunk lmplot](/figure/posts/2015-02-26-testrmark/lmplot-4.png) 

$$ \mathcal{L}(\theta) = \prod_{i=1}^{n} (1-\alpha \beta \gamma) $$

