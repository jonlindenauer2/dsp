[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)


```
import scipy.stats

# men: 5'10" to 6'1", loc=178, scale = 7.7
# convert heights to inches and then centimeters
low_ht = ((5 * 12) + 10) * 2.54
upper_ht = ((6 * 12) + 1) * 2.54

# calc lower and upper percentiles of Normal dist CDF
low_p = scipy.stats.norm.cdf(low_ht, loc=178, scale=7.7)
upper_p = scipy.stats.norm.cdf(upper_ht, loc=178, scale=7.7)

# calc percentage range of US males within BMG height restrictions
pct_in_range = upper_p - low_p

print('Percentage of US males in Blue Man Group height requirement is',
      "{:.1%}".format(pct_in_range))
```
Percentage of US males in Blue Man Group height requirement is 34.3%
