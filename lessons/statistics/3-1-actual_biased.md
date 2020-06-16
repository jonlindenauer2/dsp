[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

```
# read in female response data and create PMF for the actual data
resp = nsfg.ReadFemResp()
pmf_num_kids = thinkstats2.Pmf(resp.numkdhh, label='actual')
pmf_num_kids
```
Pmf({0: 0.466178202276593,<br/> 1: 0.21405207379301322,<br/> 2: 0.19625801386889966,<br/> 3: 0.08713855815779145,<br/> 4: 0.025644380478869556,<br/> 5: 0.01072877142483318},<br/> 'actual')
```
print('mean of actual', "{:.2f}".format(pmf_num_kids.Mean()))
print('variance of actual', "{:.2f}".format(pmf_num_kids.Var()))
```
mean of actual 1.02 <br/>
variance of actual 1.41
```
thinkplot.Hist(pmf_num_kids)
```

```
biased_pmf_num_kids = BiasPmf(pmf_num_kids, label='observed')
biased_pmf_num_kids
```
Pmf({0: 0.0, 1: 0.20899335717935616, 2: 0.38323965252938175, 3: 0.25523760858456823, 4: 0.10015329586101177, 5: 0.052376085845682166}, 'observed')
```
print('mean of observed', "{:.2f}".format(biased_pmf_num_kids.Mean()))
print('variance of observed', "{:.2f}".format(biased_pmf_num_kids.Var()))
```
mean of observed 2.40 <br/>
variance of observed 1.17
```
thinkplot.Hist(biased_pmf_num_kids)
```

```
thinkplot.PrePlot(2)
thinkplot.SubPlot(2)
thinkplot.Pmfs([pmf_num_kids, biased_pmf_num_kids])
thinkplot.Show(xlabel='number of children',
              axis = [-1, 6, 0, .5])
```


