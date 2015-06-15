---
layout: page
title: "R tips"
comments: yes
---

> Here I present some `R` tips and tricks I have learned from various resources over the years.

***

* For math styles in `R` plots. Thanks to [@RLangTip](https://twitter.com/RLangTip)
{% highlight r %}
demo(plotmath)
{% endhighlight %}

***

* Converting a matrix of characters into numeric
{% highlight r %}
mat <- matrix(c("5","6","7","8","hello","world"),ncol=3)
class(mat) <- "numeric"
{% endhighlight %}

***

* Running the equivalent of `knitHTML` in `RStudio` on the command line. Note you must install [pandoc first](https://github.com/rstudio/rmarkdown/blob/master/PANDOC.md#newer-systems-debianubuntufedora)
{% highlight r %}
rmarkdown::render("source.Rmd")
{% endhighlight %}

***

* Passing command line arguments using `rmarkdown::render()`. Thanks to [sjackman](https://github.com/rstudio/rmarkdown/issues/319)  

**source.Rmd**
{% highlight r %}
```{r}
args <- commandArgs(trailingOnly = TRUE)
args[1]+args[2]
```
{% endhighlight %}

**command line**
{% highlight bash %}
Rscript -e 'rmarkdown::render("source.Rmd")' 0.5 0.7
{% endhighlight %}

***

* Rendering `HTML` documents with [`knitrBootstrap`](https://github.com/jimhester/knitrBootstrap) on the command line. Thanks to [lcolladotor](http://lcolladotor.github.io/derfinder/derfinder.html#Reproducibility)

**source.Rmd**
{% highlight r %}
---
output:
  html_document:
    toc: true
    theme: united
  knitrBootstrap::bootstrap_document:
    theme.chooser: TRUE
    highlight.chooser: TRUE
---

<!--
%\VignetteEngine{knitr::rmarkdown}
%\VignetteIndexEntry{Some title here}
-->

Testing `knitrBootstrap`
==================================

```{r}
args <- commandArgs(trailingOnly = TRUE)
args[1]+args[2]
```
{% endhighlight %}

**command line**
{% highlight bash %}
Rscript -e 'library(knitrBootstrap);library(rmarkdown);render("source.Rmd", "knitrBootstrap::bootstrap_document")' .05 .07
{% endhighlight %}

*be careful of the single quotes and double quotes: it matters!*

***

* Testing for the presence of elements in one vector in another, i.e., the opposite of `%in%`

{% highlight r %}
"%ni%" <- Negate("%in%")
c(2,3) %ni% c(2,4,5)
[1] FALSE  TRUE
{% endhighlight %}

***

* How the `bs` function works for B-splines in `R` by [Samiran Sinha](http://www.stat.tamu.edu/~sinha/research/note1.pdf)

***

* Find records which occur in table 1 but not in table 2 using `anti_join` in `dplyr`. Thanks to [ZevRoss](http://zevross.com/blog/2014/08/05/using-the-r-function-anti_join-to-find-unmatched-records/)

{% highlight r %}
library(dplyr)

d <- Titanic %>% as.data.frame

(d1 <- d[1:5,])
  Class    Sex   Age Survived Freq
1   1st   Male Child       No    0
2   2nd   Male Child       No    0
3   3rd   Male Child       No   35
4  Crew   Male Child       No    0
5   1st Female Child       No    0

(d2 <- d[2:6,])
  Class    Sex   Age Survived Freq
2   2nd   Male Child       No    0
3   3rd   Male Child       No   35
4  Crew   Male Child       No    0
5   1st Female Child       No    0
6   2nd Female Child       No    0

anti_join(d1,d2, by=c("Class","Sex","Age"))
  Class  Sex   Age Survived Freq
1   1st Male Child       No    0
{% endhighlight %}

*** 

* Rendering `.Rmd` posts for site built with [Jekyll](http://jekyllrb.com/) using the [servr](http://cran.r-project.org/web/packages/servr/index.html) package. In your website directory create a folder called `_knitr` and place the [build.R](https://github.com/yihui/knitr-jekyll/blob/gh-pages/build.R) script in there. Place the `.Rmd` file which contains the contents of your post in the `_source` directory of your website folder. Then from the root folder of your website run the following command:

{% highlight r %}
servr::jekyll(script = "_knitr/build.R", serve = FALSE)
{% endhighlight %}










