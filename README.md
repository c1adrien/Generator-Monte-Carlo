# Economic scenario generators
- We propose a detailed sensitivity analysis of the embedded parameters of a GSE, namely the correlation matrix of risk factors. The impact of these parameters on the VIF and the BE is calculated for a benchmark ALM model.
- We propose MICE, a deep learning model that calculates visually interpretable sensitivity indices.
- We classify market data using a variational autoencoder (implicit volatility surfaces for European options and swaptions) to refine the impact of parameters based on market regimes.

# Factor analysis: accelerating the procedure through learning methods
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

# Market data classification with a VAE
### Framework Implemented
We built a Bayesian Variational Autoencoder (VAE) to generalize PCA on swaption volatility surfaces: $X=\{x_1, \ldots, x_N\}$, i.i.d. samples generated by $z$. The assumptions are: $z \sim \mathcal{N}(0, I)$ and $x \sim p_\theta(x \mid z)$. We approximate $q_\phi(z \mid x) \approx \mathcal{N}\left(z ; \mu^{(i)}, \sigma^{(i)}\right)$ with $\mu^{(i)}$ and $\sigma^{(i)}$ estimated by neural networks. VAEs offer generative capabilities and capture non-linearities better than PCA. The figure below shows the reconstruction of implied volatility surfaces for at-the-money call options with different maturities, using data from Refinitiv.


# Application: Sensitivity Analysis of a GSE

Main impact results of different factors on the VIF
- Swaption volatilities: Over 50%
- Market data for CALL options: Around 30%
- Interest rate model shift: 0.4%
- Correlations: 0.2%
- Embedded GLMM parameters: 0.1%

The thesis also details the behavior of embedded parameters when market data changes (and for the SCR).

Potential future applications
The main idea we bring forward is to recalibrate sensitive parameters only when the market context changes enough for these parameters to have a real impact on the VIF or SCR.

Accurately predicting the value of the SCR or VIF based on market data is complex due to the evolving nature of ALM models. However, our work can be used to anticipate which parameters to monitor when the market regime changes.

We also propose the use of our work to calculate new sensitivity indices. In particular, we have developed a new deep learning model that is simple to train and has the advantage of being interpretable. This model, based on copulas, can be used to calculate complex sensitivities where the underlying distributions are multimodal.
