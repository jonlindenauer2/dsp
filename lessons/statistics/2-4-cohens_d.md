[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

I wrote Cohen's d code so I could better understand the mechanics of what this statistic was calculating:
##### my Cohen's D
```
diff = firsts.totalwgt_lb.mean() - others.totalwgt_lb.mean()

var_first = firsts.totalwgt_lb.var()
var_others = others.totalwgt_lb.var()
n_first = len(firsts.totalwgt_lb)
n_others = len(others.totalwgt_lb)

pooled_var = (n_first * var_first + n_others * var_others) / (n_first + n_others)

cohens_d = diff / pooled_var**.5

print('Mean first baby weight is', "{:.2f}".format(firsts.totalwgt_lb.mean()))
print('Mean other baby weight is', "{:.2f}".format(others.totalwgt_lb.mean()))
print("Cohen's d is", "{:+.2f}".format(cohens_d))
```
Output:
Mean first baby weight is 7.20 <br/>
Mean other baby weight is 7.33 <br/>
Cohen's d is -0.09

I am comparing the birth weights of the first baby to other subsequent babies. The mean of the first baby weight is 7.2 lbs.
The mean of the other baby weight is 7.33 lbs. It appears the other baby weight is slightly higher (~2%) than the first baby
weight. The output for Cohen's d is -0.09. This Cohen's d statistic tells us how big (or small) the difference is between
the two means we are comparing on a standard deviation scale. Most statistical literature states that a Cohen's d less than
0.2 is trivial (or no effect is present). The Cohen's d of -0.09 that was calculated for our comparison implies that there
is no difference between first and other baby's weight.
