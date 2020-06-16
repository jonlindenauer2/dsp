[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

The discussion regarding biasing of survey questions because of a poor sampling plan, or the lack of knowledge of how the data was acquired, is very important for data analytics. Without this knowledge, the analysis can lead to incorrect conclusions. The example we have is that our survey asked the female respondents how many children they had. The survey also asked the children how many children were their family.
```
# read in female response data and create PMF for the actual data
resp = nsfg.ReadFemResp()
pmf_num_kids = thinkstats2.Pmf(resp.numkdhh, label='actual')
pmf_num_kids
```
Pmf({0: 0.466178202276593,<br/> 1: 0.21405207379301322,<br/> 2: 0.19625801386889966,<br/> 3: 0.08713855815779145,<br/> 4: 0.025644380478869556,<br/> 5: 0.01072877142483318},<br/> 'actual')

The actual results for the PMF above show that 46% of the females responded that they did not have children. 21% had 1 child and 20% had 2 children. The mean number of children is 1 (displayed below) for the actuals.
```
print('mean of actual', "{:.2f}".format(pmf_num_kids.Mean()))
print('variance of actual', "{:.2f}".format(pmf_num_kids.Var()))
```
mean of actual 1.02 <br/>
variance of actual 1.41
```
thinkplot.Hist(pmf_num_kids)
```
The histogram of the actual number of children shows an exponential decreasing number.<br/>
Click on the ? to show histogram, and back arrow in upper left of window to get back.
!['Click ?'](https://github.com/jonlindenauer2/dsp/tree/master/img/hist1.png)

```
biased_pmf_num_kids = BiasPmf(pmf_num_kids, label='observed')
biased_pmf_num_kids
```
Pmf({0: 0.0,<br/> 1: 0.20899335717935616,<br/> 2: 0.38323965252938175,<br/> 3: 0.25523760858456823,<br/> 4: 0.10015329586101177,<br/> 5: 0.052376085845682166},<br/> 'observed')

The observed (biased) results PMF for the children (shown above) has 0% saying there were no children. 21% said 1 child, 38% said 2 children and 25% said 3 children. The mean number of children is 2.4 (displayed below) for the observed. This is more than double the actual mean result. The variability of the two samples, as measured by the variance, is fairly equivalent. This is good and allows us to calculate Cohen's d (effect size).

```
print('mean of observed', "{:.2f}".format(biased_pmf_num_kids.Mean()))
print('variance of observed', "{:.2f}".format(biased_pmf_num_kids.Var()))
```
mean of observed 2.40 <br/>
variance of observed 1.17
```
thinkplot.Hist(biased_pmf_num_kids)
```
The histogram of the observed number of children shows a different distribution from the actual data.<br/>
Click on the ? to show histogram, and back arrow in upper left of window to get back.
!['Click ?'](https://github.com/jonlindenauer2/dsp/tree/master/img/hist2.png)
```
thinkplot.PrePlot(2)
thinkplot.SubPlot(2)
thinkplot.Pmfs([pmf_num_kids, biased_pmf_num_kids])
thinkplot.Show(xlabel='number of children',
              axis = [-1, 6, 0, .5])
```
The histogram of the observed overlaid with the actual data for number of children shows the observed is biased upward.<br/>
Click on the ? to show histogram, and back arrow in upper left of window to get back.
!['Click ?'](https://github.com/jonlindenauer2/dsp/tree/master/img/hist3.png)

```
# Cohen's D
diff = pmf_num_kids.Mean() - biased_pmf_num_kids.Mean()

var_act = pmf_num_kids.Var()
var_obs = biased_pmf_num_kids.Var()
n_act = len(pmf_num_kids)
n_obs = len(biased_pmf_num_kids)

pooled_var = (n_act * var_act + n_obs * var_obs) / (n_act + n_obs)

cohens_d = diff / pooled_var**.5

print("Cohen's d is", "{:+.2f}".format(cohens_d))
```
Cohen's d is -1.21 <br/>

The Cohen's d effect size is -1.21. According to the statistical literature, an effect size greater than 0.8 is large.
Therefore this effect size is large and indicates the observed data is biased.
