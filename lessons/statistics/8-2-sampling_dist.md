[Think Stats Chapter 8 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77) (scoring)

Plot of sample distribution of estimate L (Lambda) of an exponential distribution of size n=10 and λ=2.
```
def SimulateSampleExp(lam, n, iters):
    lams = []
    for j in range(iters):
        xs = np.random.exponential(1.0/lam, n)
        L = 1 / np.mean(xs)
        lams.append(L)
    return lams

lams = SimulateSampleExp(2, 10, 1000)

cdf = thinkstats2.Cdf(lams)
thinkplot.Cdf(cdf)
thinkplot.Config(xlabel='Sample Lambda',
                 ylabel='CDF')
```
The CDF plot of the exponential distribution of n=10 and λ=2:
<br/>
Click on the ? to show plot, and back arrow in upper left of window to get back.
!['Click ?'](https://github.com/jonlindenauer2/dsp/tree/master/img/sample_lambda_cdf.png)<br/>
<br/>
Calculate and print the standard error of the Lambda estimate and the 90% confidence interval.
```
def RMSE2(estimates, actual):

    e2 = [(estimate-actual)**2 for estimate in estimates]
    mse = np.mean(e2)
    return np.sqrt(mse)

rmse_lams = RMSE2(lams, 2)
pctl_5 = np.percentile(lams, 5)
pctl_90 = np.percentile(lams, 95)

print("The standard error of the Lambda est is", "{:.3f}".format(rmse_lams))
print("The 90% confidence interval of the Lambda est is", "{:.3f}".format(pctl_5), "to", 
      "{:.3f}".format(pctl_90))
```
The standard error of the Lambda est is 0.831<br/>
The 90% confidence interval of the Lambda est is 1.297 to 3.638<br/><br/>
Calculate and print the standard error of the Lambda estimate and the 90% confidence intervals
for n = 10, 50, 250, 500, 1000<br/>
```
n_inc = {10: [0, 0, 0], 50: [0, 0, 0], 250: [0, 0, 0], 500: [0, 0, 0], 1000: [0, 0, 0] }

for key in n_inc:
    lams = SimulateSampleExp(2, key, 1000)
    rmse_lams = RMSE2(lams, 2)
    pctl_5 = np.percentile(lams, 5)
    pctl_90 = np.percentile(lams, 95)
    n_inc[key] = [rmse_lams, pctl_5, pctl_90]
    print('n =', key, 'std err =', "{:.2f}".format(n_inc[key][0]), 
          '90% CI =','(',"{:.2f}".format(n_inc[key][1]), ',', 
          "{:.2f}".format(n_inc[key][2]), ')')
```
n = 10 std err = 0.75 90% CI = ( 1.23 , 3.49 )<br/>
n = 50 std err = 0.29 90% CI = ( 1.59 , 2.55 )<br/>
n = 250 std err = 0.12 90% CI = ( 1.81 , 2.23 )<br/>
n = 500 std err = 0.09 90% CI = ( 1.85 , 2.16 )<br/>
n = 1000 std err = 0.07 90% CI = ( 1.90 , 2.11 )<br/><br/>
The standard error and confidence intervals shrink as n increases.
