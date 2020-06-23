[Think Stats Chapter 8 Exercise 3](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77)

---

```
# function that takes a goal-scoring rate, lam, in goals per game, and simulates a game by 
# generating the time between goals until the total time exceeds 1 game, then returns the 
# number of goals scored.
def SimulateGame(lam):

    goals = 0
    t = 0
    while True:
        time_between_goals = random.expovariate(lam)
        t += time_between_goals
        if t > 1:
            break
        goals += 1

    # estimated goal-scoring rate is the actual number of goals scored
    L = goals
    return L
    
# set goal scoring rate to 2 goals per game
L_actual = 2
L_hat = SimulateGame(L_actual)
print('Estimated goals scored for single game is', L_hat)
```
Estimated goals scored for single game is 2 <br/>
```
# simulate 100,000 times to get distribution of sample estimate L_hat
def Estimated3(L_actual, m):
    L_hat_lst = []
    i = 0
    
    for i in range(m):
        L_hat = SimulateGame(L_actual)
        L_hat_lst.append(L_hat)
        
    return L_hat_lst
    
L_actual = 2
m = 100000

L_hat_lst = Estimated3(L_actual, m)

# calc mean error of estimate
def MeanError2(estimates, actual):
    errors = [estimate - actual for estimate in estimates]
    return np.mean(errors)
    
# compute the mean error and RMSE
mean_err_L_hat = MeanError2(L_hat_lst, L_actual)
rmse_L_hat = RMSE2(L_hat_lst, L_actual)
print('The mean error is', mean_err_L_hat)
print('The RMSE is', "{:.3f}".format(rmse_L_hat))    
```
The mean error is 0.0035 <br/>
The RMSE is 1.410 <br/>
```
# plot the sampling distribution of the estimate L_hat
cdf = thinkstats2.Cdf(L_hat_lst)
thinkplot.Cdf(cdf)
thinkplot.Config(xlabel='Lambda Hat',
                 ylabel='CDF')
```
Click on the ? to show plot, and back arrow in upper left of window to get back.
!['Click ?'](https://github.com/jonlindenauer2/dsp/tree/master/img/goal_scored_samp_dist.png)<br/>
<br/>
```
# calc 90% CI
pctl_5 = np.percentile(L_hat_lst, 5)
pctl_90 = np.percentile(L_hat_lst, 95)

print("The 90% confidence interval of the Lambda Hat is", "{:.3f}".format(pctl_5), "to", 
      "{:.3f}".format(pctl_90))
print('The std err is', "{:.3f}".format(rmse_L_hat))
```
The 90% confidence interval of the Lambda Hat is 0.000 to 5.000<br/>
The std err is 1.414
```
# what happens to sampling error for increasing values of lambda?
L_actual_lst = [2, 4, 6, 8]
m = 100000

for lam in L_actual_lst:
    L_hat_lst = Estimated3(lam, m)
    mean_err_L_hat = MeanError2(L_hat_lst, lam)
    rmse_L_hat = RMSE2(L_hat_lst, lam)
    print('The mean error is', mean_err_L_hat, 'for actual lambda of', lam)
    print('The RMSE is', "{:.3f}".format(rmse_L_hat), 'for actual lambda of', lam)
```
The mean error is 0.00025 for actual lambda of 2<br/>
The RMSE is 1.409 for actual lambda of 2<br/>
The mean error is -0.01286 for actual lambda of 4<br/>
The RMSE is 1.994 for actual lambda of 4<br/>
The mean error is -0.00784 for actual lambda of 6<br/>
The RMSE is 2.451 for actual lambda of 6<br/>
The mean error is -0.00452 for actual lambda of 8<br/>
The RMSE is 2.828 for actual lambda of 8<br/>
<br/>
The bias of the lambda estimate does not change much as the actual lambda increases,
but the standard error does increase.

---
