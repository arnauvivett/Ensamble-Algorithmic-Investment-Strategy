A point to be critical of this model, is the fact that I've assumed to have an infinite reservoir of money such that 
big loses don't influence my ability to invest more. Not considering the money that is held at any moment in time can be risky.


There are also a few assumptions that I made during the creation of this algorithm that should be assessed in future versions as well. 
First, the clustering algorithm could be changed by another one that is more reliable and also more parameters could be computed to perform 
the clustering analysis. The minimum number of nodes per community is also arbitrary and the experiment time range that I've considered is 
also arbitrary. There are many more markets in the world from which I picked a very particular one from the US. Although this choice is based 
on the fact that I am interested in markets with high correlation, it is always a good idea to diversify to other countries.


Another critical point is that there are two things that I can't explain, the first one (which has already been commented) being the fact 
that the algorithm works better when using the deviation of stock $k$ instead of the deviation of the ensemble. The other thing is that the
returns landscape have a preference for large window times and specially small values of alpha. One possible explanation may be due to more 
trades being done, since I am considering daily data, not hourly or in seconds, the model might find optimum low alphas since doing more 
trades accumulate more error and thus produce larger benefit.

Finally, the Sharpe ratio for the different weights of the communities could be used to optimize for expected return and volatility. And a risk
analysis is missing.
