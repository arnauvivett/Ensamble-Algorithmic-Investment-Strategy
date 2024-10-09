# Trading Logic

Now that for every stock in the community, there is a corresponding ensemble mean, 
which is essentially common to every stock but has been re-scaled, it can be used to 
generate trading signals in the following manner. Using a very similar definition to 
$S_{k}^{\pm\sigma}$, the moving threshold is defined with an extra parameter $\alpha$ 
which will become important now.  

$$\theta_k^{\pm} = S_k^e(t)\pm\alpha \sigma_k(t)$$

This threshold, will be used to generate the trading signals to long and short the stock 
$S_k(t)$. To illustrate how the algorithm works look at the following figure: 

<img width="759" alt="trading_logic" src="https://github.com/user-attachments/assets/8740e204-bb7b-4373-9f73-bf9bc1270ecc">
This figure showcases how a single stock is traded. Red dots indicate that the stock is 
being shorted, while blue dots, indicate that the stock is being longed. Green dots mean 
that the position is being closed


 This particular case has been cherry-piked as to show how the algorithm looks like 
 when it is making a profit. It is basically profiting the difference from when it opens 
 a position to when it closes it. It can also make a negative profit if it opens a position
 shorting for instance whose closing value is much higher than that of the opening value. 
 In this case, since the stock was shorted at a lower price than it was closed, the difference 
 in price is what is lost. 

 Here it is also where the $\alpha$ parameter becomes important since it essentially allows 
 us to choose what is the right threshold at which open positions. The higher it is, the less 
 likely it will be the price reaches it, but the more profit will be made.

Another important detail, is that the benefit produced by a trade on this algorithm, 
can either be saved and invest a fixed quantity every time, or the gain can be reinvested. 
If the gain is reinvested, then it will gain much more, but also at the cost of loosing much more. 

### Half Life

Finally, the last thing is to assign each stock a weight based on it's half life. This is a measure 
of stationarity in time series, since the process described above is essentially a mean reverting 
process, higher weights or trading volume should be assigned to those stocks that tend to mean revert
faster. To compute the half life, I essentially turn the stock prices minus the global mean; 
$y(t) = S_k(t)-S_k^e(t)$, into an Ornstein-Uhlenbeck  formula for the mean reverting process, 
$y(t) = (\lambda y(t-1)+\mu)dt+d\epsilon$. This allows to get an analytic solution for the expected
value: 
$$E(y(t))=y_0 e^{\lambda t} - \mu/\lambda (1-e^{\lambda t})$$

If $\lambda$ is negative (as in a mean reverting process), then the expected value decays to the 
value $-\mu/\lambda$. From here the half life is simply $H=\frac{log(2)}{\lambda}$. This coefficient
is computed for every $y(t)$ in the community and they are ranked like: 
$$w_k = \frac{1/H_k}{\sum_{k\in C} \frac{1}{H_k}}$$

Those coefficients will be multiplicative of the returns made by each stock in the community.

$y(t) = S_k(t)-S_k^e(t)$

$y(t) = (\lambda y(t-1)+\mu)dt+d\epsilon$

$H=\frac{log(2)}{\lambda}$

### Strategy optimization and testing

Now joining everything so far, the trading strategy is complete for the testing time. 
Putting everything together, the logic is implemented for every stock in every community 
found in the SP500 stocks. 
Not only that but for every any value of alpha and window size, the returns can be computed. 
If an exhaustive search is done for the surface that is represented by those parameters, 
then the maximum return can be found. Exactly at the point 
of maximum return, the data is used for the test part. 

In this case starting from 2015-01 until 2022-06, the maximum of $0.23$ occurs at a window of $120$ days 
and an alpha parameter of $0.3$.


The algorithm is simply run again with the values that maximized the training for the dates 2022-06 until 2024. The training 
was done completely independently of the testing. One has to be really careful not to mix data 
of the test in any of the training steps otherwise, the estimation of the return will obviously
be biased. 
In this case, the returns for the maximum values computed before are of $0.29$. This can be compared with
the returns of longing the same communities found in training and summing 
all the returns from that time. The returns are $0.106 $. To be fair, is unusually low.
By market standards it should be around the $20\%$. 


This strategy also outputs unusually high returns for that time windows, by checking other times
with varying windows, from 2000 to 2007, the market returns 0.26 and the strategy only 0.02.
From 2007 to 2010, the market returns 0.36, and the strategy 0.14. From 2010 to 2015, the market returns 0.17,
the strategy 0.10. From 2015 to 2018 the market returns 0.17 the strategy 0.10. 



