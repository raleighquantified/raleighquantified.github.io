---
layout: post
title:  "Using Machine Learning to Predict Whether Demolished Homes Will Be Rebuilt"
---
![_top100.yml]({{ site.baseurl }}/images/corrmapall.png)

<h2>Introduction</h2>

Since 2000, about four thousand permits have been filed for the demolition of residential properties in the City of Raleigh. Given the relatively high value of Raleigh real estate, I assumed that most of these homes were being demolished to make room for new planned development, or that developers would swoop in to find some new use for the land on which they sat. 

However, when I looked at the data, I found that for a narrow majority of these properties, there was no record of their ever having been replaced. What could account for this? I had been itching to work on a classification problem anyway, so I decided to train a random forest model in order to get some sense of:

1. The extent to which demolition and rebuilding patterns predictable.

2. The most important "risk factors" that predict whether a given property will be rebuilt and never replaced. 

<h2>Preparing the Data</h2>

I used the same building permit data I used for a couple of my earlier analyses (here and here), and all the caveats I mentioned in those posts are obviously relevant here too. In this case, preparing the data was even trickier, in that I had to come up with a systematic way to determine whether a demolished building had had another built in its place.

Identifying properties that had been demolished and never replaced was straightforward. I simply looked for addresses that were only associated with one permit a piece, and then filtered out non-demolition permits.

The approach I took to identifying properties that had been replaced was more of a methodological stretch but (I think) still highly defensible. 

Essentially, I found addresses associated with exactly two permits --one a demolition permit, the other a building permit. After sorting and briefly scanning the resulting dataframe, I found that this approach had (at least for the most part) correctly identified demolished-and-replaced properties. 

One objection might be that I probably missed some properties that had been demolished a rebuilt multiple times. I'm glad to concede that I probably missed a few, but most properties were associated with only one or two permits, so I wasn't that concerned about it. 

<h2>Feature Selection and Engineering</h2>

I had a number of different columns to work with, but only a few proved useful to me for a couple of reasons:

1. My main goal was identifying general trends, so I constrained myself to using features that were anchored to these trends. Administrative elements (permit numbers, information about contractors,etc.) of individual permit records may have actually improved the accuracy of my model, but it wasn't clear that they would illuminate anything about the City overall. 

2. There was considerable collinearity between many of the dataset's existing features. For example, one-hot encoding zip codes failed to add much predictive value, as I had already included other, better location-identifying features.

As a starting point, I just included latitude and longitude coordinates, estimated project cost, and the year and month that the permit was issued. This model was accurate about 70% of the time, but I thought I might be able to do better.

**Density of Street Development**

A variable called "street number" seemed improve the model marginally, and I assumed that this was because, for higher street number, it helped the model identify streets where a lot of development had been done, which seemed relevant.

Going back to the original dataset, I decided to engineer a feature called "Number of Permits," as I thought this would more reliably capture the amount of development that had happened on a given street, and it seemed to perform marginally better than street number.

**Crime**

I started thinking about other datasets that I could bring in, and I remembered that Raleigh Open Data maintains a datset of crime reports. I figured that crime was probably highly correlated with any number of socioeconomic variables, some of which would surely be relevant, so I gave it a try.

Using regex, I was able to get a simple count of the number of crimes reported at each street name. This seemed to add some value, and normalizing for street density by dividing the count by the number of total permits on the relevant street worked even better. 

To get a better sense of how well different models would perform, I ran a few a hundred times each, splitting the training and test data each time, and visualized the ranges of their accuracy scores:

![_top100.yml]({{ site.baseurl }}/images/models_rotated_labels.png)


The basic model used only my starting variables (latitude, longitude, estimated project cost, year, and month), and the one on the far right is called "Kitchen Sink," because I threw in everything but that. In fact, here's the correlation map:

![_top100.yml]({{ site.baseurl }}/images/corrmapall.png)

Intestingly, street number seems to be correlated with latitude, which seems to confirm that it isn't the purest metric for density.

This is the correlation map for the model I ended up choosing:

![_top100.yml]({{ site.baseurl }}/images/corrmap.png)

<h2>Important Features</h2>

Now I want to look at the relative importance of different features, according to my model. I'll go from most to least significant. 

Latitude and Longitude

Estimated Project Cost

Crimes per Permit for Street

Number of Permits for Street

Year and Month








