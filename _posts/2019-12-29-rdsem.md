# Residual Structural Equation Modeling --- A short sketch

---

This document is an informal introduction to---and a subsequent literature review of---[residual] dynamic structural equation modeling ([R]DSEM) of (intensive) longitudinal data. Although [R]DSEM is mostly applied to multi-level problems wherein the within- and between-person differences are modeled, here I assume these sources of variations can be disentangled. Then I will demonstrate how a simple, non-hierarchical, case of such models can be implemented using R package `lavaan`. *This post is not complete yet, as of 29 Dec 2019.*

Without some [basic knowledge of factor analysis](https://en.wikipedia.org/wiki/Factor_analysis)---or, SEM with latent variables/measurement models---the reader might find the text a bit cryptic. Nonetheless, I will first review the factor analysis formally. Let's first see how FA/SEM works in non-longitudinal data. If you are aquainted with FA, you can safely skip the next section. However, although it may seem tedious, I suggest not doing so because I use a similar notation afterwards.

Before moving on, notice that I use vertical vectors in this post, and to write them as transpose ($^\top$) of horizontal vectors to fit inline typesetting---sorry if that is too confusing.

# Conventional R-factor analysis: Modeling between-persons differences

Latent variable modeling (LVM) tries to estimate a (multidimensional) latent construct---AKA *factor*---that is believed to have "caused" the variations obsereved in a measurement made on a sample. This factor need not actually exist; it can be an abstract reification of processes involved in generating the variations observed in the data, and one need not make any ontological commitments to their actual existence---what does it mean to exist by the way?

I know many psychmetricians/psychologists/philosophers would disagree with what I just mentioned. I believe this disagreement (at least partly) lies in the definition of (ontological) existence and causality. I take on a mechanistic approach towards explanation of phenomenon (as discussed in my master thesis in AI, which I will link it here when I publish it online) and with my interpretation of "vertical causation".


Anyways.

The classic case of LVM is R-factor analysis, wherein cross-sectional measurements of $p$ variables in a sample of $N$ individuals is analyzed to find out whether some (abstract) "entities" (i.e., factors) can *explain* the variations in the data collected from the individuals---if people differ in their responses, there should be something there to cause their differences, right?

Suppose you have collected some intensive longitudinal data of a participant and now you have a set of $p$-dimensional vector of manifest variables (that are manifested in the measurement; also known as *items* in the context of psychometrics) $Y_{n \times 1} = [y_{1}, y_{2}, \ldots, y_{m}]^\top$.

The idea is, if an $m$-dimensional latent variable $\Theta_{m \times 1}$ can explain the variations in $y_i$s among the individuals, then the following system of equations would hold (assuming zero intercepts, i.e., centered variables, for thye sake of simplicity):

$$
\begin{equation}
\left\{
\begin{array}{ll}
y_1 = \lambda_1 \Theta + \epsilon_1 \\
y_2 = \lambda_2 \Theta + \epsilon_2 \\
\vdots \\
y_n = \lambda_n \Theta + \epsilon_n \\
\end{array}
\right.
\label{eq:systemofeqs}
\tag{1}
\end{equation}
$$

Where $\lambda_i$ are $1 \times m$ vectors of *loadings*, showing how much $\Theta$ is present (or *manifested*) in variable $y_i$. $\epsilon_i$s are the residual terms of the regressions. Since this system of equations consists of linear regression models, the assumptions of such models (most importantly, normality, independence, and homoscedasticity of residuals) should hold.
The individual differences of the subjects $j$ and $k$ then will be summarized in their estimated $\Theta^j$ and $\Theta^k$.

In a (more elegant) matrix notation, we have:

$$
\begin{equation}Y_{p \times 1} = \Lambda_{p \times m} \Theta_{m \times 1} + E_{p \times 1}
\label{eq:rfactor}
\tag{2}
\end{equation}$$

Wherein $\Lambda_{{n \times m}} = [\lambda^\top_{1}, \lambda^\top_{2}, \ldots, \lambda^\top_{n}]^\top$ is the loading matrix. $E_{{n \times 1}} = [\epsilon_{1}, \epsilon_{2}, \ldots, \epsilon_{n}]^\top$, usually referred to as _meassurement errors_, basically encapsulates the unexplained variations of items that the factor model could not capture. remembering assumptions of regression models, it has to be normally distributed. normally distributed. More formally, $E \sim \mathcal{N}(0, \Psi)$, wherein $\Psi_{p \times p}$ is the covariance matrix of the residuals. Independence of error terms imply that $cov(\epsilon_i, \epsilon_{j \neq i}) = 0$. Hence, $\Psi$ is diagonal matrix:

$$
\begin{equation}
\Psi_{p \times p} =
\begin{bmatrix} 
\psi_{11} & 0 & \ldots & 0 \\
0 & \psi_{22} & \ldots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & 0 & \psi_{pp}
\end{bmatrix}
\label{eq:coverror}
\tag{3}
\end{equation}
$$

However, the covariance matrix of the manifest variables (i.e., $S_{p \times p}$) is, in general, non-diagonal.

The factor structure (explained in the system of linear regressions models), *if* $\Theta_i$s are known, implies a covariance matrix $\Sigma_{p \times p}$. However, we do not know $\Theta_i$s---they are *latent* after all. Hence, in order to estimate $\Theta$, one can try to make $\Sigma$ as similar as possible to $S$.

To do so, let the covariance matrix of the latent variables be $\Phi_{m \times m}$. Playing with the system of regression models, it can be shown that the following holds:

$$
\begin{equation}
\Sigma = \Lambda \Phi \Lambda^\top + \Psi
\label{eq:sigma}
\tag{4}
\end{equation}
$$

Eventually, we are interested in $\Lambda$. However, we also have to estimate $\Phi$, and $\Psi$ to identify the model. 


To do so, $\Sigma$ (as defined by $\Lambda$, $\Phi$, and $\Psi$ in $\eqref{eq:sigma}$) is estimated to resemble the actual covariance matrix of measurements as mush as possible. This can be done by minimizing the fit function $F_{ML}$ through maximum likelihood estimation:

$$
\begin{equation}F_{ML} = ln(|S|) - ln(|\Sigma|) + trace[(S)(\Sigma^{-1})] - p
\label{eq:maximumlikelihood}
\tag{5}
\end{equation}$$

So, the estimations and calculations go as follows:

$$
\begin{equation}
Y \rightarrow S \xrightarrow{\text{ML}} \Lambda, \Phi, \& \Psi \xrightarrow{\Lambda \& Y^j} \Theta^j
\label{eq:estimations}
\tag{7}
\end{equation}
$$

This estimation requires fixing some of the parameters to make the model identifiable; otherwise, the *unknowns* (i.e., parameters) outnumber the *knowns* (i.e., equations), and there would be infinite number of equivalent models. Usually, this is done by fixing variances of certain latent variables or some loadings to 1.

Note that one can (manually) set some elements of the loading matrix to zero (so that some factors do are not manifested in some $y_i$s), set some elements of the latent covariance matrix to zero, or allow non-zero off-diagonal elements of $S$. The latter is known as factor models with structured residuals, and can be shown to be equivalent to including another factor to the model (hence not violating the independence assumption in $E$).

One can add additional equations to the system of regression models to model additional relations (mostly regressions) between the latent variables and other manifest variables. Such models---that have more than factor models---are called *structural equation models* wherein the factor parts of them are called *measurement models*.

What if we wanted to find factors underlying within-person variations of the manifest variables? This is discussed in what follows.

# P-factor analysis: Explaining within-persons variations

Now suppose that, instead of measuring a sample of a population, you have measured variables of one person at different times, e.g., have measured their emotions over the course of a year, and want to model the idiographic process underlying variations in the manifest variables.

More formally, suppose you have collected some intensive longitudinal data of a participant and now you have an $p$-dimensional multivariate time series, say, $Y^t_{n \times 1} = [y^t_{1}, y^t_{2}, \ldots, y^t_{n}]^\top$ at times $0 \lt t \lt T$ . Now you want to model the $m$-dimensional latent constructs 'causing' the measured values, i.e., $\Theta^t_{m \times 1} = [\theta^t_{1}, \theta^t_{2}, \ldots, \theta^t_{m}]^\top$. Similar to R-factor analysis, you might want to write a factor model for each time as

$$
\begin{equation}
Y^t_{p \times 1} = \Lambda^t_{p \times m} \Theta^t_{m \times 1} + E^t_{p \times 1}
\label{eq:p-factor}
\tag{8}
\end{equation}$$

As in R-factor analysis, the loading matrix (here, $\Lambda^{t}$) should be shared by all observations (here, for all $t$s), hence $\Lambda^{t} = \Lambda$.

So far so good? **No!**

Like R-factor analysis, the assumptions of linear regression must hold. Again, most importantly, the residuals should be independent at times $t_i$ and $t_j$ In other words, $cov(\epsilon_{t_i}, \epsilon_{t_j \neq t_i}) = 0$---and it is not necessarily the case.

Conventionally, the simple/classic P-factor analysis ignores the serial temporal dependencies between measurements. 


***[To be completed later](https://hackmd.io/@psyguy/r1skOakUr)***

# A short literature review

Most of the research in this area (at least those enumerated here) belong to psychology and social sciences.

- A) Hamaker, E. L., Asparouhov, T., Brose, A., Schmiedek, F., & Muthén, B. (2018). **At the frontiers of modeling intensive longitudinal data: Dynamic structural equation models for the affective measurements from the COGITO study**. _Multivariate behavioral research_, 1-22. https://doi.org/10.1080/00273171.2018.1446819

- B) Driver, C. C., Oud, J. H., & Voelkle, M. C. (2017). **Continuous time structural equation modeling with R package ctsem**. http://dx.doi.org/10.18637/jss.v077.i05

- C) Driver, C. C., & Voelkle, M. C. (2017). **Introduction to Hierarchical Continuous Time Dynamic Modelling With ctsem**. _R package Vignette_. Available online at: https://cran.r-project.org/web/packages/ctsem/index.html.

- D) Driver, C. C. (2018). **Hierarchical Continuous Time Dynamic Modelling for Psychology and the Social Sciences**. https://doi.org/10.18452/18927

- E) McNeish, D. (2018). **A Primer on Two-Level Dynamic Structural Equation Models for Intensive Longitudinal Data**. _PsyArXiv preprint_ https://doi.org/10.31234/osf.io/j56bm

- F) Asparouhov, T., Hamaker, E. L., & Muthén, B. (2018). **Dynamic structural equation models**. _Structural Equation Modeling: A Multidisciplinary Journal_, 25(3), 359-388. https://doi.org/10.1080/10705511.2017.1406803
	
- G) Asparouhov, T., & Muthén, B. (2019). **Comparison of models for the analysis of intensive longitudinal data**. http://www.statmodel.com/download/RDSEM.pdf
	
- H) Poncela, P., & Ruiz, E. (2012). **More is not always better: back to the Kalman filter in dynamic factor models**. https://www.ucm.es/data/cont/docs/518-2013-11-05-Poncela_Jun4.pdf
	
- I) McAlinn, K., Rockova, V., & Saha, E. (2018). **Dynamic Sparse Factor Analysis**. _arXiv preprint_ arXiv:1812.04187. https://arxiv.org/abs/1812.04187
	
- J) Holmes, E. E., Scheuerell, M. D., and Ward, E. J. (2019). **Applied Time Series Analysis for Fisheries and Environmental Sciences**. https://nwfsc-timeseries.github.io/atsa-labs/
	
- K) Bianconcini, S., & Bollen, K. A. (2018). **The Latent Variable-Autoregressive Latent Trajectory Model: A General Framework for Longitudinal Data Analysis**. _Structural Equation Modeling: A Multidisciplinary Journal_, 25(5), 791-808. https://doi.org/10.1080/10705511.2018.1426467
	
- L) Hamaker, E. L., Dolan, C. V., & Molenaar, P. C. (2003). **ARMA-based SEM when the number of time points T exceeds the number of cases N: Raw data maximum likelihood**. _Structural Equation Modeling: A Multidisciplinary Journal_, 10(3), 352-379. https://doi.org/10.1207/S15328007SEM1003_2

- M) Voelkle, M. C., Oud, J. H., von Oertzen, T., & Lindenberger, U. (2012). **Maximum likelihood dynamic factor modeling for arbitrary N and T using SEM**. _Structural Equation Modeling: A Multidisciplinary Journal_, 19(3), 329-350. https://doi.org/10.1080/10705511.2012.687656

- N) Molenaar, P. C., & Nesselroade, J. R. (2009). **The recoverability of P-technique factor analysis**. _Multivariate Behavioral Research_, 44(1), 130-141. https://doi.org/10.1080/00273170802620204

## A quick review of these references

**A** lacks the measurement model and consequently does not take into account AR at measurement level. [Mplus]

**B**, **C**, belong to ctsem R package developed in **D**, which is Driver's Ph.D. dissertation. Driver claims ctsem is capable of dynamic factor analysis. However, the suggested measurement model assumes serial independence of manifest residuals (in contrast to, e.g., RDSEM). So this cannot be used in our problem. (Driver and I [had a discussion on twitter.](https://twitter.com/_psyguy/status/1118794063472361472)) [R]

**E** briefly addresses the trended data but lacks measurement model (and consequently, residual AR). [Mplus]

**F** is a (rather comprehensive) tutorial to DSEM which also (rather briefly) addresses RDSEM. It has an appendix on RDSEM estimation which helps better understand the model. In short, they break down the error/residual term and consequently form "a special case of the DSEM model where the residual variables are modeled as within-level latent variables." [Mplus]

**G** is a better, more detailed comparison of DSEM and RDSEM. [Mplus]

**H** and **I** are good texts explaining DFMs. The former discusses the role of serial and contemporaneous idiosyncratic noise (~ residuals in RDSEM context) and how to include it in the model. [R]

**J** discusses DFM in more details with additional examples in R but doesn't go deep in residual AR as far as I've noticed. [R]

**K** is a great reference discussing building such AR models (as called Latent Variable-Autoregressive Latent Trajectory, LV-ALT models). [no implementation]

**L** is an interesting case of ARMA (D)SEM but still does not moel residual temporal dependencies. [Mx]

**M**, good to be comapred with **L**, is an integration of two approaches: "standard time series analysis ($T$ large and $N = 1$) and conventional SEM ($N$ large and $T = 1$ or small)," and addresses ergodicity too. It does not model residual serial dependencies however. [OpenMx]

Finally, one should also cf. **N** for evidence supporting robustness of P-factor analysis in time series of affect. If this is true for a multivariate time series, one does not need to deal with complicated (D)SEM models. [Nonlis] 

# The solution

***[To be completed later](https://hackmd.io/@psyguy/r1skOakUr)***
