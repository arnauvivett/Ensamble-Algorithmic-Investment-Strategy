# Ensamble Creation


The first thing that is done, is to import the market data from a library in python called "yahoo finance" from an initial to a final date. The data is first cleaned by deleting those time series that have more than $5\%$ missing data and fill the rest with the values of the previous days. Then the data is  separated into training and testing. Lets first consider how the model is trained. To create the ensembles, the return and the volatility of every stock is first computed using:

$$R = \langle \frac{S(t_1)-S(t_0)}{S(t_0))} \rangle \times \Delta$$ 

$$V = \sqrt{Var\left( \frac{S(t_1)-S(t_0)}{S(t_0))}\right) \times\Delta}$$

Where the $\Delta$ is the time difference between the initial and final times of each stock price. Ii is assumed that those two variables characterize the statistical properties of the stocks in some meaningful way. For this reason, k-means clustering is then performed on the data produced. Although k-means has some disadvantages such as being sensitive to the initial choice of parameters, difficulty handling outliers and the need to know the number of clusters in advance, it is also simple to scale, has guaranteed convergence and is also simple to implement.

The data within the clusters is then used to evaluate what is the mutual information between the different time series that have fallen into the same cluster. To do so, the joint probabilities and product of marginals is first computed for every pair of time series within the same cluster.  

This produces a matrix with the correlation between every stock, which can be interpreted as a graph, and clusters can be found using the "Louvain method". The advantage of this method is that the time compleixty is only of $O(n\log n)$ and does not have free parameters. At the same time, it is not deterministic which may be a problem for some applications. 

As a side note, I have tried calculating the null value of the model, but in this case it didn't make sense, the time series are long and they clearly show a pattern that is not random. In the null model the joint probability of the shuffled version of the data is essentially the same as the marginal, so the mutual information becomes zero. 
