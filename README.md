# Economic scenario generators
- We propose a detailed sensitivity analysis of the embedded parameters of a GSE, namely the correlation matrix of risk factors. The impact of these parameters on the VIF and the BE is calculated for a benchmark ALM model.
- We propose MICE, a deep learning model that calculates visually interpretable sensitivity indices.
- We classify market data using a variational autoencoder (implicit volatility surfaces for European options and swaptions) to refine the impact of parameters based on market regimes.


### Why look for new sensitivity indices?  
The first-order Sobol index $S_i$ measuring the contribution of the variable $\mathbf{X}_{\mathbf{i}}$ in the model $Y=\eta(\mathbf{X})$ is given by

$$
S_i=\frac{V\left[\mathbb{E}\left(Y \mid X_i\right)\right]}{V(Y)}
$$

This model is unsuitable for multimodal distributions, as is the case in our applications. One approach is to use a coefficient based on mutual information, $\rho_{MI}\left(X_1, X_2\right)=\sqrt{1-\exp\left[-2MI\left(X_1, X_2\right)\right]}$, where $MI(X, Y)=H(Y)-H(Y \mid X)$ is the mutual information and $H$ is the Shannon entropy.

### Estimation of mutual information  
An important contribution of the thesis is to note that the relationship between copulas and mutual information can be expressed as follows:

$$
M I(X, Y) = E_{(U, V) \sim c(u, v)}[\log c(U, V)]
$$

where $X = F_1^{-1}(U)$ and $Y = F_2^{-1}(V)$. We propose a Deep Learning model to learn to simulate the pair $(U, V)$ and to learn the density $c(u, v)$ in order to directly determine the mutual information.
