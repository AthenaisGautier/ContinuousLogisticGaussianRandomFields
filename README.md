# Continuous logistic Gaussian random measure fields for spatial distributional modelling
### By Athenais Gautier and David Ginsbourger

This repository contains the code and data associated with our paper titled "Continuous logistic Gaussian random measure fields for spatial distributional modelling". The detailed research can be accessed through our preprint: [arXiv:2110.02876](https://arxiv.org/abs/2110.02876).

## Abstract

We study Spatial Logistic Gaussian Process (SLGP) models for non-parametric estimation of probability density fields using scattered samples of heterogeneous sizes. 
SLGPs are examined from the perspective of random measures and their densities, investigating the relationships between SLGPs and underlying processes.
Our inquiries are motivated by SLGP's abilities in delivering probabilistic predictions of conditional distributions at candidate points, allowing conditional simulations of probability densities, and jointly predicting multiple functionals of target distributions. 
 We demonstrate that SLGP models induced by continuous GPs exhibit joint Gaussianity of their log-increments, enabling us to establish theoretical results regarding spatial regularity. Additionally, we extend the notion of mean-square continuity to random measure fields and establish sufficient conditions on covariance kernels underlying SLGPs to ensure these models enjoy such regularity properties.
Finally, we propose an implementation using Random Fourier Features and showcase its applicability on synthetic examples and on temperature distributions at meteorological stations.

## Continuity modulus of SLGPs

[The considered vignette can be read here](https://htmlpreview.github.io/?https://github.com/AthenaisGautier/ContinuousLogisticGaussianRandomFields/blob/main/vignetteUnconditional.html)

In the main body of the paper, we make the following claim:

For $D \subset \mathbb{R}^{d_D}$ a compact and convex index space with $d_D\geq 1$, we prove the following
result:
 
**Condition 1**

There exist $C, \alpha_1, \alpha_2>0$ such that for all $\mathbf{x},
\mathbf{x'}; \in D, t, t' \in \mathcal{T}$:

$$k([\mathbf{x}, t], [\mathbf{x}, t]) + k([\mathbf{x}',
t'],[\mathbf{x}', t']) - 2 k([\mathbf{x}, t],
[\mathbf{x}', t']) \leq C \cdot \max(\Vert \mathbf{x}-
\mathbf{x}' \Vert_\infty ^{\alpha_1}, \Vert t - t' \Vert_\infty
^{\alpha_2})$$

**Theorem 2**

Consider the SLGP $Y$ induced by a centred GP $Z$ with covariance kernel $k$: 

$$Y_{\mathbf{x}, t} := \dfrac{e^{Z_{\mathbf{x},
t}}}{\int_\mathcal{T}e^{Z_{\mathbf{x}, u}} \,d\lambda(u) } \text{ for
all } (\mathbf{x}, t) \in D \times \mathcal{T}
$$

and assume that $k$ satisfies the condition above.


Then, for all $\gamma>0$ and $0<\delta < \gamma\alpha_1/2$ (for the first two Equations, resp. $0<\delta < \gamma\alpha_1$ for the last two Equations), there exists $K_{\gamma, \delta}>0$ such that for all $\mathbf{x}, \mathbf{x}' \in D^2$:  

$$ \mathbb{E} \left[ d_{H}({Y}_{\mathbf{x}, \cdot}, {Y}_{\mathbf{x}', \cdot})^\gamma \right] \leq K_{\gamma, \delta}  \Vert \mathbf{x} - \mathbf{x}' \Vert^{\gamma \alpha_1 /2 -\delta}_\infty$$

$$ \mathbb{E} \left[ V({Y}_{\mathbf{x}, \cdot}, {Y}_{\mathbf{x}', \cdot})^\gamma \right] \leq K_{\gamma, \delta}  \Vert \mathbf{x} - \mathbf{x}' \Vert^{\gamma \alpha_1/2 -\delta}_\infty$$

$$ \mathbb{E} \left[ KL({Y}_{\mathbf{x}, \cdot}, {Y}_{\mathbf{x}', \cdot})^\gamma \right] \leq K_{\gamma, \delta}  \Vert \mathbf{x} - \mathbf{x}' \Vert^{\gamma \alpha_1 -\delta}_\infty$$

$$ \mathbb{E} \left[ d_{TV}({Y}_{\mathbf{x}, \cdot}, {Y}_{\mathbf{x}', \cdot})^\gamma \right] \leq K_{\gamma, \delta}  \Vert \mathbf{x} - \mathbf{x}' \Vert^{\gamma \alpha_1 -\delta}_\infty $$


Where for two pdfs $f_1$, $f_2$ on $\mathcal{T}$:

* $d_{H}$ denotes the Hellinger distance: $d_H(f_1, f_2) := \sqrt{\frac{1}{2}\int_\mathcal{T} \left( \sqrt{f_1(u)} - \sqrt{f_2(u)} \right)^2 \,du}$

* $KL$ denotes the Kullback-Liebler divergence: $KL(f_1, f_2) := \int_\mathcal{T} f_1(u) \log\left( f_1(u) / f_2(u)\right) \,du$

* $V$ denotes a squared log-ratio dissimilarity: $V(f_1, f_2) := \int_\mathcal{T} \left( \log \frac{ f_1(u)}{f_2(u)}\right)^2 \,du$

* $d_{TV}$ denotes the Total Variation distance: $d_{TV}(f_1, f_2) := \int_\mathcal{T} \left\vert f_1(u) - f_2(u) \right\vert \,du$


## Posterior consistency of SLGP-based density estimation

[The considered vignette can be read here](https://htmlpreview.github.io/?https://github.com/AthenaisGautier/ContinuousLogisticGaussianRandomFields/blob/main/vignetteConsistency.html)

## A meteorological application on real-world data

[The considered vignette can be read here](https://htmlpreview.github.io/?https://github.com/AthenaisGautier/ContinuousLogisticGaussianRandomFields/blob/main/vignetteMeteo.html)
