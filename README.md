# Continuous logistic Gaussian random measure fields for spatial distributional modelling

This repository contains the code and data associated with our paper titled "Continuous logistic Gaussian random measure fields for spatial distributional modelling". The detailed research can be accessed through our preprint: [arXiv:2110.02876](https://arxiv.org/abs/2110.02876).

## Abstract

We study Spatial Logistic Gaussian Process (SLGP) models for non-parametric estimation of probability density fields using scattered samples of heterogeneous sizes. 
SLGPs are examined from the perspective of random measures and their densities, investigating the relationships between SLGPs and underlying processes.
Our inquiries are motivated by SLGP's abilities in delivering probabilistic predictions of conditional distributions at candidate points, allowing conditional simulations of probability densities, and jointly predicting multiple functionals of target distributions. 
 We demonstrate that SLGP models induced by continuous GPs exhibit joint Gaussianity of their log-increments, enabling us to establish theoretical results regarding spatial regularity. Additionally, we extend the notion of mean-square continuity to random measure fields and establish sufficient conditions on covariance kernels underlying SLGPs to ensure these models enjoy such regularity properties.
Finally, we propose an implementation using Random Fourier Features and showcase its applicability on synthetic examples and on temperature distributions at meteorological stations.

