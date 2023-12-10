---
layout: page
title: Movies in time
cover-img: /assets/img/time.png
thumbnail-img: /assets/img/time.png
share-img: /assets/img/time.png

---

## Introduction

All things on earth exist under the cold cruel hands of father Time, and the movie industry is no exception. It’d be easy to think that we, as intelligent beings, 
are above the concept of temporal bias, that the weather has no influence on our perception of movies and that in the Oscar season, the movie we vouch for is 
obviously our favorite, and not just the freshest in our memory. In actuality, our perception of a movie, just as our perception of a meal, can be very contextual, 
and what better context than time itself. We think that there are some correlations between a movie’s success and its release date within different time-frames and 
that the producers know it, and exploit it. Our goal is to show how us simple creatures are influenced by time in our perception of movies, and what are the 
strategies movie studios use to benefit from this bias, whether it's expressed within a month, a year, a decade or a lifetime. To this end, we need to ask ourselves 
a couple of questions. 

---

{% include movie_world_map.html %}

![A great image](/assets/img/n_movie_per_day.png)



## Best Relase date analysis


In this part, we're trying to figure out the ideal release date for movies that ensures the best performance at the box office. Our analysis covers data spanning from 1897 to 2012 across 87 countries.

Our primary method is regression analysis, examining if there's a connection between the 'release month' and the 'box office' performance. The formula we use is:
$$Y = \beta_0 + \beta_1x_1 + \beta_2x_2 + ... + \beta_{11}x_{11}$$

$Y$ = Box office \
$X$ = Dummies variable of release month (Note: here we use December as bench mark)

![A great image](/assets/img/Screenshot 2023-12-10 at 17.09.42.png)


### Instructions of the dynamic model above
The value of blue bars is the coefficient value of $\beta_0,\beta_1,\beta_2,...\beta_{11}$, which is referred to the left-sided y-axis.\
The value of orange points is the t-value each of corresponding coefficient, which is referred to the right-sided y-axis.\
The value of red line (1.96) is used to check the significant of the coefficient under 95% confidence, which is referred to the right-sided y-axis. (e.g. if the t-value stay outside the interval [-1.96,1.96], then the corresponding coefficient is significant)

### Identifying the Best Month
After conducting regression for all 87 countries from 1897 to 2012, we observed that June consistently yields a significantly higher average Box Office compared to other months. This pattern persists when we perform the same analysis for countries with over 200 data points during the same period. However, the best month varies for specific countries; for the US and Germany, it's still June, but for the UK and France, it is July. Notably, the coefficients for Canada and Korea aren't significant, suggesting they don't offer valuable insights.
Our initial assumption is that June and July are generally the best release months for generating higher box office returns.

### Genre-Specific Analysis
We expand investigation to different genres while still using data from all 87 countries from 1897 to 2012, finding that most genres, such as Drama, Comedy, and Romance films, support our hypothesis that June and July are optimal release months. However, certain genres like Black-and-white films defy this trend, possibly due to their 'old school' nature, making them different from typical movies.

Then we try to find the best week during the month.

![A great image](/assets/img/Screenshot 2023-12-10 at 17.09.59.png)



