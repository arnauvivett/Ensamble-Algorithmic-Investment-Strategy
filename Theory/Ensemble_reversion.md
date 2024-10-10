# Ensamble Reversion

Now that the ensembles with similar statistical properties have been selected, what will be
computed now is the ensemble average and standard deviation through a time window, for 
every community found before. To do so, for all the stocks, their rolling
mean (or moving average) is:

$$R(S_k(t)) =\frac{1}{W} \sum_{i=0}^{n-1} S_k(t_{W-i})$$

Where $W$ is the rolling window. Notice that to be consistent with the notation, 
I am using the index $k$ to state that it is a particular stock from the community 
being considered. The standard deviation can be computed similarly: 

$$\sigma_k(t) = \sqrt{\frac{\sum_{t_i} (S_k(t_i)-R(S_k(t_i)))^2}{n-W}}$$ 

The z-score normalization is also used to normalize the price and thus produce an stationary 
time series. 

$$S^{st}_k(t) = \frac{S_k(t)-R(S_k(t))}{\sigma_k(t)}$$

Finally, the ensemble stock is computed using the mean of all the normalized stocks 
from the community. 

$$S_e^{st}(t) = \frac{1}{N_S} \sum_{k\in C} S_k^{st}(t)$$

The ensemble stock's standard deviation can be computed as well by using the following formula: 

$$\sigma_e(t) = \sqrt{\frac{1}{N_S} \sum_{k\in C} (S_k^{st}-S_e^{st})^2}$$

Which is also stationary. Now, in order to use this ensemble mean to generate trading signals, 
it must be scaled back to every stock's price. What is meant is that, that the price will 
be monitored in reference to a transformed ensemble mean. Using the z-score formula, 
the ensemble mean from the point of view of a single stock, will look like: 

$$S_k^{e}(t) = S_e^{st}(t)*\sigma_k(t) + R(S_k(t))$$ 

The exact same expression can be used to calculate the standard deviation bounds from above as
$S_{k}^{\pm\sigma}=S_{e}^{st}\pm\sigma_e(t)$ and thus this equation can 
be used to bring the value back to the scale of whatever stock it is being traded.

<img width="772" alt="ensamble_price" src="https://github.com/user-attachments/assets/923daa58-3602-4f56-ab90-4cf46f0c8c41">
Where the ensamble mean is shown in white ant the standard deviation in red.


That is what made most sense to me mathematically. But empirically I found that the if instead 
of computing $S_{k}^{\pm\sigma}$, the way it is just explained, it is computed using the $\sigma_k(t)$ 
from eq(\ref{sigma_k}), the benefits of the whole algorithm go from near zero, to more than $20\%$. 
Thus, I choose to use the formula with the high returns even though its a problem I haven't been 
able to solve. 

$$S_{k}^{\pm\sigma}=S_{e}^{st}\pm\sigma_k(t)$$

The inverse transform looks like: 
<img width="759" alt="inverse_scale_transform" src="https://github.com/user-attachments/assets/04833f52-313a-455e-b0f9-fa47d64bbd9f">

