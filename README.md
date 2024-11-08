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

$$ \mathbb{E} \left[ d_{H}(Y_{\mathbf{x}, \cdot}, Y_{\mathbf{x}', \cdot})^\gamma \right] \leq K_{\gamma, \delta}  \Vert \mathbf{x} - \mathbf{x}' \Vert^{\gamma \alpha_1 /2 -\delta}_\infty
$$

$$ \mathbb{E} \left[ V(Y_{\mathbf{x}, \cdot}, Y_{\mathbf{x}', \cdot})^\gamma \right] \leq K_{\gamma, \delta}  \Vert \mathbf{x} - \mathbf{x}' \Vert^{\gamma \alpha_1/2 -\delta}_\infty
$$

$$ \mathbb{E} \left[ KL(Y_{\mathbf{x}, \cdot}, Y_{\mathbf{x}', \cdot})^\gamma \right] \leq K_{\gamma, \delta}  \Vert \mathbf{x} - \mathbf{x}' \Vert^{\gamma \alpha_1 -\delta}_\infty
$$

$$ \mathbb{E} \left[ d_{TV}(Y_{\mathbf{x}, \cdot}, Y_{\mathbf{x}', \cdot})^\gamma \right] \leq K_{\gamma, \delta}  \Vert \mathbf{x} - \mathbf{x}' \Vert^{\gamma \alpha_1 -\delta}_\infty 
$$


Where for two pdfs $f_1$, $f_2$ on $\mathcal{T}$:

* $d_{H}$ denotes the Hellinger distance: $d_H(f_1, f_2) := \sqrt{\frac{1}{2}\int_\mathcal{T} \left( \sqrt{f_1(u)} - \sqrt{f_2(u)} \right)^2 \,du}$

* $KL$ denotes the Kullback-Liebler divergence: $KL(f_1, f_2) := \int_\mathcal{T} f_1(u) \log\left( f_1(u) / f_2(u)\right) \,du$

* $V$ denotes a squared log-ratio dissimilarity: $V(f_1, f_2) := \int_\mathcal{T} \left( \log \frac{ f_1(u)}{f_2(u)}\right)^2 \,du$

* $d_{TV}$ denotes the Total Variation distance: $d_{TV}(f_1, f_2) := \int_\mathcal{T} \left\vert f_1(u) - f_2(u) \right\vert \,du$

<img src="https://github.com/AthenaisGautier/ContinuousLogisticGaussianRandomFields/blob/main/figures/ratesHolder.png" alt="Illustration of the rates" width="700"/>



## Posterior consistency of SLGP-based density estimation

[The considered vignette can be read here](https://htmlpreview.github.io/?https://github.com/AthenaisGautier/ContinuousLogisticGaussianRandomFields/blob/main/vignetteConsistency.html)

This vignette is about exploring the posterior consistency of Spatial Logistic Gaussian Processes (SLGPs) in estimating response distributions given predictor values. 


To assess the performance of SLGP-based models, we define four reference probability density fields. These fields are generated as realizations of finite-rank SLGPs. The hyperparameters of these SLGPs are known and consistent across all four references. However, the spatial regularity of these fields varies and enables us to explore the impact of spatial regularity on the performance of SLGP-based models and assess their ability to capture the underlying structure of the data.

<img src="https://github.com/AthenaisGautier/ContinuousLogisticGaussianRandomFields/blob/main/figures/ref_fields2.png" alt="The four reference fields" width="700"/>

 We then draw samples from these references and evaluate the performance of SLGP-based models. This phase involves conducting inference experiments under various conditions to comprehensively assess the models' ability to recover the underlying distributions.
 
* Reference Fields: we consider four distinct reference probability density fields.

* Levels of Smoothness: we consider different SLGP modeling, corresponding to the different kernel functions used in generating the reference fields.
  * Exponential Kernel: This kernel parametrizes GPs whose realizations are continuous but not differentiable. It produces fields with rough spatial structures.
  * Matérn 3/2 Kernel: Known for parametrizing GPs whose realizations are once continuously differentiable, this kernel generates fields with moderate smoothness.
  * Matérn 5/2 Kernel: This kernel parametrizes GPs that are twice continuously differentiable, resulting in smoother fields compared to the Matérn 3/2 kernel.
  * Gaussian Kernel: Also known as the Radial Basis Function (RBF) kernel, this kernel parametrizes GPs whose realizations are infinitely differentiable, producing fields with very smooth spatial structures.

* Number of Basis Function Frequencies: We work with various numbers of basis functions in the parametrization of the SLGP, determined through the Random Fourier Features (RFF) method. We compare having 25, 50, 100, 250 or 500 basis frequencies, and twice as many basis functions (one sine, one cosine for each frequency).
* Sample Sizes: we work with a range of sample sizes, varying from 5 to 10000000 data points.

To ensure the robustness of our results and mitigate the impact of random seed variability, we perform 100 repetitions for each experimental setting. This comprehensive experimental design leads to a total of:
$$
\underbrace{100}_{\text{Repetitions}} \times 
\underbrace{4}_{\text{Reference Models}} \times 
\underbrace{4}_{\text{Levels of Smoothness}} \times 
\underbrace{5}_{\text{Number of Basis Functions}} \times 
\underbrace{20}_{\text{Sample Sizes}} = 160,000 \text{ experiments}
$$

We assess the quality of our SLGP-based model estimations using an Integrated Hellinger distance to measure dissimilarity between two probability density valued fields $f(\mathbf{x}, \cdot)$ and $f'(\mathbf{x}, \cdot)$:

$$
d_{IH}^2(f(x, \cdot) , f'(x, \cdot) ) = \frac{1}{2}\int_D \int_T \left( \sqrt{f(\mathbf{v}, u)} - \sqrt{f'(\mathbf{v}, u))}  \right)^2 \,du \,d\mathbf{v}
$$

In the following Figure, we display the distribution of $d_{IH}$ between true and estimated fields in our experimental design.

<img src="https://github.com/AthenaisGautier/ContinuousLogisticGaussianRandomFields/blob/main/figures/consistency-distance2.png" alt="Illustration of the quality of the estimation evolving with sample size and number of features" width="700"/>

We display the MAP estimates of the density fields for different sample sizes within a well-specified SLGP setting. 


<img src="https://github.com/AthenaisGautier/ContinuousLogisticGaussianRandomFields/blob/main/figures/ref4mod4nFreq500.png" alt="Evolution of the estimation" width="700"/>

## A meteorological application on real-world data

[The considered vignette can be read here](https://htmlpreview.github.io/?https://github.com/AthenaisGautier/ContinuousLogisticGaussianRandomFields/blob/main/vignetteMeteo.html)
