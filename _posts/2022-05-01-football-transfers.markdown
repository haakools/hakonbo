---
layout: post
title:  "Ad Hoc Analysis of Transfer Fee Statistics"  
date:   2022-05-01 21:55:41 +0100
categories: transfer fee
---


The last month I have been exploring the statistical relationship between football players' transfer fee related to their stats and contract length.

After reading a [reddit post](https://www.reddit.com/r/soccer/comments/sro2kb/premier_league_transfer_spending_adjusted_for/), made by u/Uuppa, where transfer fee for the English Premier League for the last 30 years where adjusted for inflation and median market growth to answer the question of how much footballers would go for today, I was inspired to start a data science project. I wanted to make a model to predict the transfer fee of a footballer based on their stats, contract length and age. One of the key parts of the model was to make it explainable, intuitive and be insightful, instead of blindly feeding swathes of data into a tensorflow or sci-kit learn neural network and let it churn. Through this process I learned to make two webscrapers using Selenium and BeauitfulSoup (one for advanced stats and another for contract length) and got more experience with data-wrangling /data-cleaning using Pandas.



# Gathering of data
To gather the wanted data, I quickly realized I could not use the same data as u/Uuppa as transfermarkt.co.uk (emphasis on the "co.uk") prints the fees in british pounds. Transfermarkt, being a german company, is only concerned with using euro and have therefore just taken *some* years exchange rate and applied it to every transfer. This makes the transfers wildly inaccurate, but fortunately this was only a problem if one were accessing transfermarkt's webpage with "co.uk". I then took the [webscraper](https://github.com/ewenme/transfers) from ewenme on github and used ".com" instead to get the accurate figures in euro.

### Tl.dr: Do not use transfermarkt.co.uk for accurate transfer fees, use transfermarkt.com

# Discoveries in Ad Hoc Analysis
After loading the data, now in euros, I tried to get a grasp of some of the pitfalls, limitation and caveats in the data. "Is there some very noticeable trends?" I asked myself. For every question I wanted answered, I always tried to rationalize what the outcome would be before I got the plots.

Firstly, I made a distribution plot all the transfers within the big five leagues. The plot below shows the sum of the transfers in for each league, as a ratio of all the five leagues spending.
![Distribution plot for Big Five Leagues 1992-2021](/images/dist_plot.png "Distribution plot for Big Five Leagues").

From the figure, some things stick out
1. The English Premier League have almost always been one of the biggest spenders
2. The French Ligue 1 and German Bundesliga 1 have been spending very low and constantly in relation to the other leagues
3. Italian Serie A spent very much at the turn of the century


Furthermore for my analysis, I wanted to adjust of the age of players. From playing games such as Football Manager quantifies the ability of football players very precisely. From this game I have numerously times read the tooltip that "players between 27 and 32 are in the prime". And my intuition agrees. When you are in your late 20s, you are still in a very good physical state without having lost that much of that youthful athletic explosiveness and one have gathered a lot of playing time to be both tactically and mentally drilled for real on-pitch football scenarios. And so I wanted to explore this: is the prime of footballers portrayed well in the transfer data?

As to not be prone to extreme outliers as transfer data entails, I concerned myself with the median. For every age at transfer, I plotted the median transfer fee, adjusted for inflation. My theory beforehand was that it would follow a log-normal-like distribution with the peak around 27, which then would have a slightly fat tail.

![Age decay](/images/agedecay.png "Distribution plot for Big Five Leagues").

I got this graph. A very, very normally distributed graph with a mean around 25. The smooth line shows the fitted gaussian, the jagged blue line shows the data and the bars in the background show how many transfers there exists at this age.  And so there are some interesting points to be made of this graph.


1. For purchases by clubs in the Big Five Leagues, around 24-26 is the most expensive signings on average of what you hear about
2. A 20 year old and a 30 year old is on average going to be equally expensive, aswell as 19 years old and 32 years old
3. The amount of transfers as a function of age shows a log normal distribution.

Here "on average" is meant in accordance to median, as to "on average what you hear about", not if you actually take the average.


This was a short write up on what I have been doing and two of the graphs I found to be very insightful and hopefully interesting for the reader. I will come with more updates as the project continues. For now I will fetch my broomstick and clean some more data.
