[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)

The exercise examines the relationship between mother's age and the birth age of their children.
```
# read data into live DF and drop any missing value
import first

live, firsts, others = first.MakeFrames()
live = live.dropna(subset=['agepreg', 'totalwgt_lb'])

# scatterplot of mothers age vs birth weight
%matplotlib inline
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

plt.scatter(live.agepreg, live.totalwgt_lb, alpha=.2, s=2)

plt.xlabel("Mothers Age")
plt.ylabel('Birth Weight')
```
The scatterplot shows the relationship between mother's age and the birth age of their children.
There does not appear to be much of a relationship given the cloud of data points.<br/>
Click on the ? to show scatter plot, and back arrow in upper left of window to get back.
!['Click ?'](https://github.com/jonlindenauer2/dsp/tree/master/img/mom_age_vs_birth_wt.png)<br/>
<br/>
A scatterplot of the mean mother's age groups vs the birth weight percentile by those groups is 
a way of displaying the relationship's in a large dataset. The following code does the ETL for display
of the scatterplot.
```
# extract the age and weight data from the live DF and drop missing values
age_wt_df = live[['agepreg', 'totalwgt_lb']]
age_wt_df = age_wt_df.dropna()

# create the group by bins and indices for plotting
bins = np.arange(10, 45, 3)
indices = np.digitize(age_wt_df.agepreg, bins)
groups = age_wt_df.groupby(indices)

# calc group mean for the mom's age and cdf for birth weights
mean_age = [group.agepreg.mean() for i, group in groups]
cdfs = [thinkstats2.Cdf(group.totalwgt_lb) for i, group in groups]

# plot the birth weight by the mean mom's age 25th, 50th and 75th percentiles
for percent in [75, 50, 25]:
    weight_percentiles = [cdf.Percentile(percent) for cdf in cdfs]
    label = '%dth' % percent
    thinkplot.Plot(mean_age, weight_percentiles, label=label)
    
thinkplot.Config(xlabel='Mothers Age',
                 ylabel='Birth Weight',
                 axis=[10, 45, 5, 9],
                 legend=False)
```

The scatterplot shows the relationship between mother's age and the birth age of their children.
There does not appear to be much of a relationship given the flat (horizontal) lines for birth
weights across mom's age for each percentile group.<br/>
Click on the ? to show scatter plot, and back arrow in upper left of window to get back.
!['Click ?'](https://github.com/jonlindenauer2/dsp/tree/master/img/mom_age_pctl_vs_birth_wt.png)<br/>
<br/>
The code below calcs the Pearson and Spearman correlation
```
# Pearson correlation between mothers age vs birth weight
mom_age = live.agepreg
birth_wt = live.totalwgt_lb
pearson_r = mom_age.corr(birth_wt, method = 'pearson')
print('Pearson r is', "{:+.3f}".format(pearson_r))
```
Pearson r is +0.069
```
# Spearman Rank correlation between mothers age vs birth weight
spearman_r = mom_age.corr(birth_wt, method = 'spearman')
print('Spearman r is', "{:+.3f}".format(spearman_r))
```
Spearman r is +0.095<br/><br/>
The Pearson and Spearman correlation coefficients (r) both are less than 0.10 indicating just a
small positive relationship between birth weight and mother's age.
