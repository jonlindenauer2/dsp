[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)

The "InterpolateSample" fcn in the book is broken, so trying to do without.
```
# set the last income entry to $1,000,000
income_df.iloc[41, 0] = 1000000
income_df = income_df.copy(deep = True)

# create the CDF with income and the cumulative percent (ps)
income_df.set_index('income')['ps'].plot()
```
Click on the ? to show CDF plot, and back arrow in upper left of window to get back.
!['Click ?'](https://github.com/jonlindenauer2/dsp/tree/master/img/income_cdf.png)
```
# calc median by the two income upper bounds around the 50th percentile
# and taking average.
median_mask = ((income_df.ps > .45) & (income_df.ps < .55))
median_income = income_df[median_mask].income.mean()

print('The median income is', "${:,.0f}".format(median_income))
```
The median income is $52,499<br/>
```
# calculate the weighted average for the mean income
wt_income_mean = np.average(income_df['income'], 
                            weights=income_df['freq'])
print('The mean income is', "${:,.0f}".format(wt_income_mean))
```
The mean income is $88,177 <br/>
The mean income is greater than the median income. This implies the income
distribution is right skewed.
```
# find percentage of incomes less than the mean income.
pct_income_lt_mean = max(income_df.ps[income_df.income < wt_income_mean])

print('Percentage of incomes less than the mean is',
     "{:.0%}".format(pct_income_lt_mean))
```
Percentage of incomes less than the mean is 72% <br/>
```
# set the last income entry to $10,000,000
income_df.iloc[41, 0] = 10000000
income_df = income_df.copy(deep = True)

# calc median by the two income upper bounds around the 50th percentile
# and taking average.
median_mask = ((income_df.ps > .45) & (income_df.ps < .55))
median_income = income_df[median_mask].income.mean()
print('The median income is', "${:,.0f}".format(median_income))

# calculate the weighted average for the mean income
wt_income_mean = np.average(income_df['income'], 
                            weights=income_df['freq'])
print('The mean income is', "${:,.0f}".format(wt_income_mean))
pct_income_lt_mean = max(income_df.ps[income_df.income < wt_income_mean])

print('Percentage of incomes less than the mean is',
     "{:.0%}".format(pct_income_lt_mean))
```
The median income is $52,499<br/>
The mean income is $302,119<br/>
Percentage of incomes less than the mean is 98%<br/>
Making the last income interval upper bound $10,000,000 causes the mean income
to increase by 243% and makes the distribution even more right skewed.
