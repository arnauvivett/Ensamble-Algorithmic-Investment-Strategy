The first thing that is done, is to import the market data from a library in python called "yahoo finance" from an initial to a final date. The data is first cleaned by deleting those time series that have more than $5\%$ missing data and fill the rest with the values of the previous days. Then I separate the data into training and testing. Lets first consider how the model is trained and then I will explain the testing part and the results. 


I know the fact that the SP500 produces annual returns of about $10$%. The method I propose, even though it is market neutral, which represents an advantage over a purely long position, aims at a better return than that of the SP500. 

#Ensemble creation

To create the ensembles, I first compute the return and the volatility of every stock in the list using:
$$
    &R = \langle \frac{S(t_1)-S(t_0)}{S(t_0))} \rangle \times \Delta\\
    &V = \sqrt{Var\left( \frac{S(t_1)-S(t_0)}{S(t_0))}\right) \times\Delta}
$$
Where the $\Delta$ is the time difference between the initial and final times of each stock price. I assume that those two variables characterize the statistical properties of the stocks in some meaningful way. For this reason, I then perform k-means clustering on the data produced. Although k-means has some disadvantages such as being sensitive to the initial choice of parameters, difficulty handling outliers and the need to know the number of clusters in advance, it is also simple to scale, has guaranteed convergence and is simple to implement.
