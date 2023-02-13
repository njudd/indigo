---
title: "ggRain package release!"
layout: post
date: 2022-11-18 18:47
projects: true
hidden: true # don't count this post in blog pagination
description: "Making rainclouds with the ggrain pacakge"
category: project
externalLink: FALSE
---

We have released a beta version of the `ggrain` package! The purpose of the package is to easily make raincloud plots in the ggplot framework with a geom. 

The package consists of a single function `geom_rain()`. Yet it is quite powerful, allowing you to modify each element, connect observations across time with lines, flank the rainclouds and color the dots with another variable. 

![image](/assets/images/time_group_cov.png)

To download the package run the code below and checkout the [vignette](https://njudd.com/raincloud-ggrain.html) to get started!


```
if (!require(remotes)) {
    install.packages("remotes")
}
remotes::install_github('njudd/ggrain')

library(ggrain)
```
