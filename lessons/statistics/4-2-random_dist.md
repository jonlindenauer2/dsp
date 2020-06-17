[Think Stats Chapter 4 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2005.html#toc41) (a random distribution)

The generation of 1000 random uniform numbers between 0 and 1 should appear Uniform.
```
# generate 1000 random uniform numbers between (0,1)
rand_nums = np.random.random(1000)
```
The PMF plot does look odd. It appears to be a block or rectangle of data. We can see that each of the 1000 values between 
0,1 has a 0.001 (1/1000) probability of occurring, as it should. This can be seen in the PMF plot in the link.

Click the ? to display the plot. Use back arrow in the top left of the window to go back.<br/>
!['Click ?'](https://github.com/jonlindenauer2/dsp/tree/master/img/ch4_ex2_pmf.png)

The CDF plot shows a straight line which means the data follows the Uniform distribution.<br/>
Click the ? to display the plot. Use back arrow in the top left of the window to go back.<br/>
!['Click ?'](https://github.com/jonlindenauer2/dsp/tree/master/img/ch4_ex2_cdf.png)
