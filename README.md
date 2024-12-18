# <img src='https://raw.githubusercontent.com/VicentePerezSoloviev/EDAspy/master/Logo%20EDAspy.png' align="right" height="150"/>

[![PyPI](https://img.shields.io/pypi/v/edaspy)](https://pypi.python.org/pypi/EDAspy/)
[![PyPI license](https://img.shields.io/pypi/l/EDAspy.svg)](https://pypi.python.org/pypi/EDAspy/)
[![Downloads](https://static.pepy.tech/badge/edaspy)](https://pepy.tech/project/edaspy)
[![Documentation Status](https://readthedocs.org/projects/edaspy/badge/?version=latest)](https://edaspy.readthedocs.io/en/latest/?badge=latest)

# EDAspy

## Introduction

EDAspy presents some implementations of the Estimation of Distribution Algorithms (EDAs) [1]. EDAs are a type of
evolutionary algorithms. Depending on the type of the probabilistic model embedded in the EDA, and the type of
variables considered, we will use a different EDA implementation.

The pseudocode of EDAs is the following:

1. Random initialization of the population.

2. Evaluate each individual of the population.

3. Select the top best individuals according to cost function evaluation.

4. Learn a probabilistic model from the best individuals selected.

5. Sampled another population.

6. If stopping criteria is met, finish; else, go to 2.

EDAspy allows to create a custom version of the EDA. Using the modular probabilistic models and the initializators, this can be embedded into the EDA baseline and used for different purposes. If this fits you, take a look on the examples section to the EDACustom example.

EDAspy also incorporates a set of benchmarks in order to compare the algorithms trying to minimize these cost functions.

The following implementations are available in EDAspy:

* UMDAd: Univariate Marginal Distribution Algorithm binary [2]. It can be used as a simple example of EDA where the variables are binary and there are not dependencies between variables. Some usages include feature selection, for example.


* UMDAc: Univariate Marginal Distribution Algorithm continuous [3]. In this EDA all the variables assume a Gaussian distribution and there are not dependencies considered between the variables. Some usages include hyperparameter optimization, for example.


* UnivariateKEDA: Univariate Kernel Estimation of Distribution Algorithm [4]. Each variables distribution is estimated using Kernel Density Estimation.


* UMDAcat: Univariate Marginal Distribution Algorithm categorical [2]. UMDA variant for categorical data, where more than two possible values per dimension are used (otherwise, use binary version).


* EGNA: Estimation of Gaussian Distribution Algorithm [5][6]. This is a complex implementation in which dependencies between the variables are considered during the optimization. In each iteration, a Gaussian Bayesian network is learned and sampled. The variables in the model are assumed to be Gaussian and also de dependencies between them. This implementation is focused in continuous optimization.


* EMNA: Estimation of Multivariate Normal Algorithm [1]. This is a similar implementation to EGNA, in which instead of using a Gaussian Bayesian network, a multivariate Gaussian distribution is iteratively learned and sampled. As in EGNA, the dependencies between variables are considered and assumed to be linear Gaussian. This implementation is focused in continuous optimization.


* SPEDA: Semiparametric Estimation of Distribution Algorithm [7]. This multivariate EDA allows estimating the density of a variable using either KDE or Gaussians, and allow dependencies between both types of variables. It is an archive-based approach where the probabilistic model is updated given the best individuals of l previous generations.


* MultivariateKEDA: Special case of SPEDA approach in which all nodes are restricted to be estimated using KDE (Gaussian nodes are forbidden) [7]. It is also an archive-based approach.


* EBNA: Estimation of Bayesian Network Algorithm [1]. This version of EDAs is used for categorical data. The probabilistic model used is a Categorical Bayesian network, where conditional dependencies between variables can be analyzed.


* BOA: Bayesian Optimization Algorithm [8]. This version of EDAs is used for categorical data. The probabilistic model used is a Categorical Bayesian network, where Bayesian Dirichlet score is used, in contrast to EBNA.


* PBIL: Population-based incremental learning [9]. This version is a modification of UMDA strategy, where the mean of the Gaussian distribution is computed not only considering the best individuals, but also the worst one. 

Some tools are also available in EDAspy such as the Bayesian network structure plotting, for visualizing the graph learnt in some of the implementations, if needed.


Although some categorical EDAs are implemented, the package is focused in continuous optimization. Below, we show a CPU time analysis for the different approaches implemented for continuous optimization. Note that the CPU time can be reduced using parallelization (available as a parameter in the EDA initialization). Reference [7] shows a comparison about the performance of the algorithms in terms of cost function minimization. 

<img src='cpu_comparison_continuous_opt.jpeg' alt="CPU time comparison for continuous optimization" title="CPU time comparison for continuous optimization"/>

## Examples

Some examples are available in https://github.com/VicentePerezSoloviev/EDAspy/tree/master/notebooks

## Getting started

For installing EDAspy from Pypi execute the following command using pip:

```bash
    pip install EDAspy
```

## Build from Source

### Prerequisites

- C++ 17 compatible compiler.
- CMake (it is needed for pybnesian dependencies).
- OpenCL 1.2 headers/library available.
- Python >=3.8, <3.11
- pgmpy, scipy, pyarrow, pybnesian, numpy, pandas, multiprocessing.

### Installation
We provide a detailed [installation guide](INSTALLATION.md) for EDAspy.

## Testing 

The library contains tests that can be executed using `pytest <https://docs.pytest.org/>`_. Install it using 
pip:

```bash
  pip install pytest
```

Run the tests with:

```bash
  pytest
```

## How to cite?

```
@article{soloviev2024edaspy,
  title={{EDAspy: An extensible python package for estimation of distribution algorithms}},
  author={Soloviev, Vicente P and Larra{\~n}aga, Pedro and Bielza, Concha},
  journal={Neurocomputing},
  pages={128043},
  year={2024},
  publisher={Elsevier}
}
```

## Bibliography

[1] Larrañaga, P., & Lozano, J. A. (Eds.). (2001). Estimation of distribution algorithms: A new tool for evolutionary computation (Vol. 2). Springer Science & Business Media.

[2] Mühlenbein, H., & Paass, G. (1996). From recombination of genes to the estimation of distributions I. Binary parameters. In Parallel Problem Solving from Nature—PPSN IV: International Conference on Evolutionary Computation—The 4th International Conference on Parallel Problem Solving from Nature Berlin, Germany, September 22–26, 1996 Proceedings 4 (pp. 178-187). Springer Berlin Heidelberg.

[3] Mühlenbein, H., Bendisch, J., & Voigt, H. M. (1996). From recombination of genes to the estimation of distributions II. Continuous parameters. In Parallel Problem Solving from Nature—PPSN IV: International Conference on Evolutionary Computation—The 4th International Conference on Parallel Problem Solving from Nature Berlin, Germany, September 22–26, 1996 Proceedings 4 (pp. 188-197). Springer Berlin Heidelberg.

[4] Luo, N., & Qian, F. (2009, August). Evolutionary algorithm using kernel density estimation model in continuous domain. In 2009 7th Asian Control Conference (pp. 1526-1531). IEEE.

[5] Larranaga, P. (2000). Optimization in continuous domains by learning and simulation of Gaussian networks. In Proc. of the 2000 Genetic and Evolutionary Computation Conference Workshop Program.

[6] Soloviev, V. P., Larrañaga, P., & Bielza, C. (2022). Estimation of distribution algorithms using Gaussian Bayesian networks to solve industrial optimization problems constrained by environment variables. Journal of Combinatorial Optimization, 44(2), 1077-1098.

[7] Soloviev, Vicente P.& Bielza, Concha & Larrañaga, Pedro (2023). Semiparametric Estimation of Distribution Algorithms for continuous optimization. IEEE Transactions on Evolutionary Computation.

[8] Martin Pelikan, David E. Goldberg, and Erick Cantú-Paz (1999). BOA: the Bayesian optimization algorithm. In Proc. of the Genetic and Evolutionary Computation Congress (pp. 525–532).

[9] Sebag, M., & Ducoulombier, A. (1998, September). Extending population-based incremental learning to continuous search spaces. In International Conference on Parallel Problem Solving from Nature (pp. 418-427). Springer.
