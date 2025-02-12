# <span style="color: #3066a0;">Derivative of wave equation</span>

## Rushan Wu

* 2014 He derived first order Freshet derivatives, higher order Fre'chet derivatives, and the full non-linear partial derivative (NLPD) that includes all the higher order terms for accoustic wave euqation:

$$
\triangledown\cdot\frac{1}{p}\triangledown p+\frac{\omega^2}{\kappa}p=0
$$


He left the generalization to elastic waves for future research and publications.

* 2014 Nonlinear Sensitivity Operator and Its De Wolf Approximation in T-matrix Formalism
* 2015 **Renormalized nonlinear sensitivity kernel and inverse thin-slab propagator in *T*-matrix formalism for wave-equation tomography**
* 2016 Non-linear parameter estimation method based on T-matrix
* 2016 Nonlinear Deghosting Based on the T-matrix Method
* 2017 New Frechet Derivative for Envelope Data and Multi-Scale Envelope Inversion
* 2018 Higher-order Rytov modeling for strong perturbation and long range propagation
* 2020 On the applicability of a renormalized Born series for seismic wavefield modelling in strongly scattering media

### Reference

* Ru-Shan Wu and Yingcai Zheng. Non-linear partial derivative and its De Wolf approximation for non-linear seismic inversion. *Geophys. J. Int.* (2014)

## No-linear sensitivity kernel for 2D wave euqation

To solve:
$$
\frac{\partial^2u}{\partial^2 t}-c^2(\mathbf{x})\Delta u=S(\mathbf{x},t)
$$
Green function in reference medium
$$
\frac{\partial^2g_0}{\partial^2 t}-c_0^2(\mathbf{x})\Delta g_0=\delta(\mathbf{x})
$$
Define:
$$
\chi(\mathbf{x})=c^2(\mathbf{x})-c_0^2(\mathbf{x})
$$
So:
$$
\frac{\partial^2u}{\partial^2 t}-c_0^2(\mathbf{x})\Delta u=S(\mathbf{x},t)+\chi(\mathbf{x})\Delta u
$$

$$
u=\int dx^2(\chi(\mathbf{x})\Delta u+S(\mathbf{x},t))g_0(\mathbf{x})\\
=\int dx^2g_0\chi(\mathbf{x})\Delta u +\int dx^2 S(\mathbf{x},t) g_0(\mathbf{x})\\
=u_0+\int dx^2g_0\chi(\mathbf{x})\Delta u
$$

Where:

* $u_0$ : wave caused by S in reference medium $c_0$
* $g_0$: green function for reference medium $c_0$ caused by $\delta (\mathbf{x})$
* u: wave caused by S in perturbed medium c
* $\chi$: model perturbation

Use born series or Frechet derivative:
$$
u=d1+d2+d3...
$$

$$
dn=(\int dx^2 g_0 \chi\Delta)^nu_0
$$
According to Aki 2002,  Green function for 3D :
$$
\ddot{g}=\delta(\mathbf{x})\delta(t)+c^2\nabla^2g
$$

$$
g(\mathbf{x},t)=\frac{1}{4\pi c^2 |\mathbf{x}|}\delta(t-\frac{|\mathbf{x}|}{c})
$$



