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



## Best Release date analysis


In this part, we're trying to figure out the ideal release date for movies that ensure the best performance at the box office. Our analysis covers data spanning from 1897 to 2012 across 87 countries.

Our primary method is regression analysis, examining if there's a connection between the 'release month' and the 'box office' performance. The formula we use is:
$$ Y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + ... + \beta_{11} x_{11} $$

$Y$ = Box office \
$X$ = Dummies variable of release month (Note: here we use December as a benchmark)

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

### Identifying the Best Week
In our study of weeks, we take week 52 as a benchmark. We regress the box office on dummies variable of the weeks across 87 countries from 1897 to 2012. Interestingly, weeks 20, 21, and 23-30 consistently show higher box office figures compared to other months, on average. Notably, weeks 23-26 correspond to June, and weeks 27-31 correspond to July.

Our regression analysis of 'box-office and week' supports our initial assumption and aligns with patterns observed in our monthly research. It's worth mentioning that the end of May (week 20, 21) and the middle of November and December (week 46, 50) also emerge as promising periods for successful box office releases.

## Oscar analysis

The choice of release date made by movie makers are not always based on making money. Sometimes, they are based on prestige, so that they can make a lot of money at a later date. In the movie industry, this prestige is materialized by the ultimate recognition : an Oscar. It is known that the submission deadline to win an Oscar is usually around the end of the year. Furthemore, it is said that the Oscar season, ranging from October to December, it the season where movie makers release their movies that are the most likely to win an Oscar. In this chatper, we will try to invesigate the effect of Oscar season.

As a stater, we will look at the distribution of Oscar over the years. 

{% include oscar_graph.html %}

As we can see on the above figure, there seem to be a clear trend of more Oscar being won by the end of the year. The trend seems rather consistent over the years, which can be explained by the fact that almot all Oscar ceremonies took place between February and April. Having observed that, the next natural question is : do movies make more Oscars when they are released at the end of the year because that's when the best movies are released ? 

As we will see from our data, the answer is probably not. At least, we can say that they are not qualitiy perceived by the public that make theses movies better than movies released the rest of the year. 

To begin our anylisis, we start by comparing the effect of releasing in all for quarters of the year on the amount of Oscar won. For each period, we need to make a propencity score matching based on relevant covariates. The table below summarizes those covariates. 

| Relevant Covariate        | Description                                      |
|------------------|--------------------------------------------------|
| Movie budget     | The financial resources allocated to a movie      |
| Release year     | The year when the movie was released              |
| Genre            | The genre of the movie                 |
| Countries        | The countries where the movie was released    |

After doing the matching on those covariate, we will verify that the following covariates are well distributed with a simple standardized mean difference test. We decided not to match on the rating, because it is not a cause of the movie's success, but a consequence of it. However, checking the distribution of the ratings is a good indicator of what the public thought of the movie. Indeed, it is possible that movies released during the Oscar season have the same budget as movies release during other seasons, but a different kind of storytelling quality. We think that the ratings could be a variable that indicate the work put on the script, as voting people are usually more implicated and will be more critical of bad stories. 

| Covariate To Check       | Description                                      |
|------------------|--------------------------------------------------|
| Rating    | The average rating of each movie      |
| Movie budget    | The year when the movie was released              |

We report that for each of the following matching, the two covariate on the table above passed the standardized mean difference test. This is an indication that the quality and budget of movies is consistent all year round. Because of that, we can affirm that every results we found on the impact of season on number of Oscars won is probably a real effect of the season.

The figure below shows the different periods of movie releases. To add on that, all cluster has statistics about the effect of that clusters period on the number of Oscars won. 

{% include kmeans_clusters_equal.html %}

As we see on the figure above, none of the seasons effects on the number of Oscars won are statistically significant. However, looking at the data, there seem to be an effect anyway. In addition to that, the last season has a p-value of 0.06, which is too big to be statistically significant, but is a solid clue that there is more at play here. 

To deepen the analysis, we will try to find better seasons than just the for quarters of the year. For that, we use the K-means algorithm with K=4. Since the goal is to get clear separation dates for our data, we will simply cluster the movies that won a Oscar based on their release date. Such a clustering gives us slightly different seasons, but a high impact on the results.

{% include kmeans_clusters_normal.html %}

As a reminder, the movies released in all clusters have a balanced distribution of rating as well as budget. The figure above shows that the beginning of the year is a bad time to release a movie if the goal is to get some Oscars. With an intercept of 0.17 and an effect size of -0.06, the impact is far from negligible. However, the more surprising result is the end of the year, which shows an effect size of 0.13 on an intercept of 0.17. This means that the average number of Oscars won during that period is almost twice as much as during the rest of the year, with variable like buget, country, genre and release year controlled. 

To conclude this analysis, we note that our K-means algorihm has considered dates like 31 of December to be far away from 01 January, even though it is just one day appart. It is possible that a good clustering ends the last day of December because the industry is based on human activities. However, to make sure that this is the case, we need a clustering that doesn't have to consider December and January as far appart. For that, we transform the days of the year as illustrated in the following animation. 

{% include day_circle_animation.html %}

With this new paradigm, we can reconsider a K-means clustering based on the coordinates of the days of the year on a unit circle. When applying the same algorithm used for the other clusters, this is what we get.

{% include kmeans_clusters_circular.html %}

The effect size of the last cluster is much smaller than it was on the previous analysis. Indeed, we have an effect size of 0.08 on an intercept of 0.17. This means that adding those January days to the cluster only diminishes the effect. Therefore, there is a strong disconnect between December and January for the prospect of winning Oscars. We also note that the effect of the first cluster is very close to the first cluster in the previous analysis. In conclusion, it seems like Oscar season is the real deal, and movie makers who want to win Oscar have a strong incentive to release their movies towards of the year. 

But is it true for every genre ? 




