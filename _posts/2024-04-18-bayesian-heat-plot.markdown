---
title: "Bayesian Heat Plot"
layout: post
date: 2024-04-18 14:20
#tag: jekyll
# image: /assets/proj_imgs/spatialcognition/img1.png
headerImage: true
projects: true
hidden: true # don't count this post in blog pagination
description: "A plot to show off your Bayes Factors" 
category: project
# author: johndoe
externalLink: false
---

The Bayesian Heat Plot is an intuitive plot to compare your Bayes Factors using Jeffrey's 1961 scale of evidence. This post shows how to make a Bayesian Heat Plot in ggplot2.

I find it a great, intuitive way to show off your Bayes Factors!

 ![img1](/assets/proj_imgs/bayesheat/BayesianHeatPlot_image_1.png)

## Background

My latest study ([preregistration](https://osf.io/rv38z)) aimed to see if an additional year of education from a natural experiment impacts long-term neural outcomes. For this, I used point null Bayes Factors in a local-randomization regression discontinuity design.

My study compared a *causal* estimate (from a natural experiment) to a *correlational* one (total years of educational attainment). Clear visualization is essential in having your message come across, to do this I came up with the Bayesian Heat Plot. I doubt I'm the first to ever think of it, after a cursory search I found something [similar](https://www.nicebread.de/a-short-taxonomy-of-bayes-factors/).

The Y-axis is your model/parameters of interest (in this case neuroimaging measures). The x-axis shows Bayes Factors which are plotted on a log scale. You can group it (in this example; causal versus correlational), yet that's not necessary. I edited the plot a bit to add a dashed line connecting the estimates and included intuitive arrows showing the direction of evidence. 

 ![img2](/assets/proj_imgs/bayesheat/BayesianHeatPlot_image_2.png)

This plot is directly inspired by Jeffrey 1961 strength of evidence criteria, seen in Figure 1 (snagged from [Gadie et. al., 2017](https://bmjopen.bmj.com/content/7/7/e014920)).

## Code to set up data and packages for plotting

Pacman is a super useful package manager. The function `p_load`  first checks if you have the package and installs it if you don't, after this it loads the package. The Bayesian Heat Plot uses a log scale for plotting, so we will transform our Bayes Factors to the log scale for plotting.

```
if (!require(pacman)){
  install.packages('pacman')
}

pacman::p_load(ggplot, heatmaply)

# a dataframe with Bayes Factors
df <- data.frame(Y = c("CT", "CT", "WMh", "WMh", "TBV", "TBV", 
                       "wFA", "wFA", "SA", "SA", "CSF", "CSF"),
                 BFs = c(0.1385, 0.1135, 0.02883, 0.03822, 0.0493, 0.2375, 
                         0.03059, 0.2710, 0.10905, 41.70, 0.04136, 80.70),
                 type = rep(c("Causal", "Correlational"),6))

# you need to log the bf's!!!
df$logBF <- log(df$BFs)

# lets put them in the right order; ggplot uses factors for that
df$Y <- factor(df$Y, levels = c("CSF", "SA", "wFA", "TBV", "WMh", "CT"))
```
## Code to make a Bayesian Heat Plot

We will walk thru each element, yet just add them together!

First we make the plot structure, we add dots with **no color** this is done as a 'hack' and we add them back later. You don't need to use the shape arg if you don't want grouping, also note you need logged BFs for the plot (these are limited with the `ylim`; yet we flip the plot later so it becomes the x-axis). Change the `base_size` if you want everything larger or smaller.

```
BayesHeat <- ggplot(df, aes(Y, logBF, shape = type))  +
  geom_point(size = 4, color = "NA") +
  ylim(-5.5, 5.5) +
  theme_classic(base_size = 20)
```

Here we add the stripes from Jeffrey which make the Bayesian Heat Plot.

```
BayesHeat <- BayesHeat +
	annotate("rect", xmin = .5, xmax = 6.5, ymin = 4.6, ymax = 5.5, alpha = .8, fill = heatmaply::RdBu(10)[1]) + # extreme evidence
  annotate("rect", xmin = .5, xmax = 6.5, ymin = 3.4, ymax = 4.6, alpha = .8, fill = heatmaply::RdBu(10)[2]) + # very strong
  annotate("rect", xmin = .5, xmax = 6.5, ymin = 2.3, ymax = 3.4, alpha = .8, fill = heatmaply::RdBu(10)[3]) + # strong
  annotate("rect", xmin = .5, xmax = 6.5, ymin = 1.1, ymax = 2.3, alpha = .8, fill = heatmaply::RdBu(10)[4]) + # substantial
  annotate("rect", xmin = .5, xmax = 6.5, ymin = 1, ymax = 1.1, alpha = .8, fill = heatmaply::RdBu(10)[5]) + # anecdotal
  annotate("rect", xmin = .5, xmax = 6.5, ymin = -1, ymax = 1, alpha = .8, fill = "white") + # no evidence either way
  annotate("rect", xmin = .5, xmax = 6.5, ymin = -1, ymax = -1.1, alpha = .8, fill = heatmaply::RdBu(10)[6]) +
  annotate("rect", xmin = .5, xmax = 6.5, ymin = -1.1, ymax = -2.3, alpha = .8, fill = heatmaply::RdBu(10)[7]) +
  annotate("rect", xmin = .5, xmax = 6.5, ymin = -2.3, ymax = -3.4, alpha = .8, fill = heatmaply::RdBu(10)[8]) +
  annotate("rect", xmin = .5, xmax = 6.5, ymin = -3.4, ymax = -4.6, alpha = .8, fill = heatmaply::RdBu(10)[9]) +
  annotate("rect", xmin = .5, xmax = 6.5, ymin = -4.6, ymax = -5.5, alpha = .8, fill = heatmaply::RdBu(10)[10])
```

Now we have the plot background with nothing on it! We add the points, on top of the stripes.

```
BayesHeat <- BayesHeat +
	geom_point(size = 4)
```

Now we add non-logged labels for Bayes Factors. Human's don't think on the logged scale, so it's best to put them back. Note we are using `scale_y_continuous` even tho this is the x-axis of the plot, this is because we haven't flipped the plot yet.

```
BayesHeat <- BayesHeat + 
  scale_y_continuous(breaks=c(-4.6, -3.4, -2.3,-1, 0, 1, 2.3,3.4,4.6), 
                     labels = c("100", "30", "10", "1", "0", "1", "10", "30", "100"))
```

Here we change the [shapes](http://www.sthda.com/english/wiki/ggplot2-point-shapes), this is only relevant if you want to group your plot. 

```
BayesHeat <- BayesHeat + 
  scale_shape_manual(values = c(16,17))
```

Lastly, we do some beautification. A lot has to do with the moving & scaling of the legend. Also, we use `coord_flip()` to flip the plot.

```
BayesHeat <- BayesHeat + 
theme(axis.line= element_blank(), axis.ticks.y = element_blank(),
        axis.text.y = element_text(color = "black"),
        legend.text = element_text(size=12),
        legend.title = element_blank(),
        legend.position = c(.954, .861),
        legend.box.just = "center",
        legend.justification = c("right", "bottom"),
        legend.margin = margin(0.5,6, 0.5, 1),
        legend.background = element_rect(colour = 'black', fill = 'white', linetype='solid', linewidth = .3)) +
  coord_flip()
```

Take a look & save your plot!!

```
BayesHeat

ggsave("~/Desktop/BayesHeat.png", BayesHeat, width = 7, height = 5, bg = "white")
```

I hope you found this tutorial helpful :) If you use it in a publication please cite the empirical study:

```
Citation holder for ROSLA UKB study
```



