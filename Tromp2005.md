# Seismic tomography, adjoint methods, time reversal and banana-doughnut kernel

Jeroen Tromp, Carl Tape and Qinya Liu

## Prior knwoledge

* Stress-strain rerlationship for elastic medium

$$
\tau_{ij}=c_{ijkl}u_{k,l}
$$

* Motion
  $$
  \rho \ddot{u}_i=f_i+\tau_{ij,j}
  $$

* Reprentation theorems for Green function (All is shown in *Aki et al., 2002* section 2.5)

  For free boundary, which means the traction due to $G$ is zero for $\xi$ in $S$
  $$
  u_n(\mathbf{x},t)=\int^{\infty}_{-\infty}d\tau\int_V f_i(\xi,\tau)G_{ni}(\mathbf{x},t-\tau;\xi)dV\\
  +\int^{\infty}_{-\infty}d\tau\int_SG_{ni}(\mathbf{x},t-\tau;\xi)T_i(\mathbf{u}(\xi,\tau),\mathbf{n})dS
  $$
  The euqation is derived from Reciprocity theorems From Eq2.34 to Eq2.40. For two pairs of fields, the boundary conditions and initial conditions of which are in general different, but their $c_{ijkl}$ is the same. There is a relationship between the two displacement and stress field:
  $$
  \int_V(\mathbf{f}-\rho\ddot{\mathbf{u}})\cdot\mathbf{v}dV+\int_S\mathbf{T}(\mathbf{u},\mathbf{n})\cdot\mathbf{v}dS\\
  =\int_V(\mathbf{g}-\rho\ddot{\mathbf{v}})\cdot\mathbf{u}dV+\int_S\mathbf{T}(\mathbf{v},\mathbf{n})\cdot\mathbf{u}dS\\
  $$
  Then change $g$,$v$ into Dirac function and Green function. We can integrate $u_n$ with Representation Theorems. Pay attenuation to the sign(plus or minus) of the body force. The plus situation is :
  $$
  \rho\frac{\partial^2}{\partial t^2}G_{in}=\delta_{in}\delta(\mathbf{x}-\mathbf{\xi})\delta(t-\tau)+\frac{\partial}{\partial x_j}(c_{ijkl}\frac{\partial G_{kn}}{\partial x_l})
  $$
  
## Scattering field

In *Hudson, 1977*. We first define the parameter of reference medium as a similar material within a domin $V_0$ with boundary $S_0$ . The structural parameters are:
$$
\rho^0,c_{ijkl}^0,\mathbf{u}^0
$$
The perturbation is defined with superscript "1":
$$
\rho=\rho^0+\rho^1,c_{ijkl}=c_{ijkl}^0+c_{ijkl}^1,\mathbf{u}=\mathbf{u}^0+\mathbf{u}^1
$$
In *Tromp et al., 2005*, it is defined as $\delta\rho$ , $\delta c_{ijkl}$ and $\delta s$.

The reference situation and original situation (with perturbation) all satisfy the equation of motion, where the body force is zero:
$$
\frac{\partial}{\partial x_j}(c_{ijpq}^0\frac{u_p^0}{x_q})-\rho^0\ddot{u}^0_i=0
$$
Similarly:
$$
\frac{\partial}{\partial x_j}((c_{ijpq}^0+c_{ijpq}^1)\frac{(u_p^0+u_p^1)}{x_q})-(\rho^0+\rho^1)(\ddot{u}^0_i+\ddot{u}^1_i)=0
$$
Upon the substituion of the latter into the former we obtain:
$$
\rho^0\ddot{u}_i^1=\underbrace{-\rho^1\ddot{u}_i+\frac{\partial}{\partial x_j}(c_{ijpq}^1\frac{u_p}{x_q})}_{body \quad force}+\frac{\partial}{\partial x_j}(c_{ijpq}^0\frac{\partial u^1_p}{\partial x_q})
$$
Pay attenuation to the sign of the body force. For this formula, the medium parameter is $\rho^0$ and $c_{ijpq}^0$ , but the displacement field is $\mathbf{u}^1$ rather than $\mathbf{u}^0$. It means that  **we can obtain the scattering field caused by the perturbation by applying a special force to the 'reference mediun with good properties', which avoids processing the complex medium after perturbation.** It's so exciting! However, we can find that $\mathbf{u}$ is contained in the body force, which means we can't get body force directly. 

Apply the Reprentation theorems from Aki to the equation, we can solve the scattering field. After correcting small mistakes in Eq3 of  *Hudson, 1977*, we obtain:
$$
u^1_l(\mathbf{x},t)=\int^\infty_{-\infty}d\tau\int_VdV[-\rho^1\ddot{u}_i(\xi,\tau)+\frac{\partial}{\partial \xi_j}(c_{ijpq}^1\frac{u_p}{\xi_q}) ] G_{li}(\mathbf{x},\mathbf{\xi},t-\tau)\\+\int^{\infty}_{-\infty}d\tau\int_SG_{li}(\mathbf{x},\xi;t-\tau)T_i(\mathbf{u}(\xi,\tau),\mathbf{n})dS \tag{scattering}
$$

Where 
$$
T_i(\mathbf{u}(\xi,\tau),\mathbf{n})=c_{ijpq}^0\frac{\partial u_p}{\partial \xi_q}n_j
$$
Using integration by parts, then change a volum integraion term surface integration:
$$
\int_V\frac{\partial}{\partial \xi_j}(c_{ijpq}^1\frac{u_p}{\xi_q})G_{li}(\mathbf{x},\mathbf{\xi};t-\tau)dV=\\\int_V\frac{\partial(c_{ijpq}^1\frac{u_p}{\xi_q})G_{li}(\mathbf{x},\mathbf{\xi};t-\tau)}{\partial \xi_j}dV-\int_V(c_{ijpq}^1\frac{u_p}{\xi_q})\frac{\partial}{\partial \xi_j}G_{li}(\mathbf{x},\mathbf{\xi};t-\tau)dV=\\
\int_Sc_{ijpq}^1\frac{u_p}{\xi_q}G_{li}(\mathbf{x},\mathbf{\xi};t-\tau)n_jdS-\int_V(c_{ijpq}^1\frac{u_p}{\xi_q})\frac{\partial}{\partial \xi_j}G_{li}(\mathbf{x},\mathbf{\xi};t-\tau)dV
$$
 Substitute the eq into Eq.scattering. Combine the surface integration and  remain the volume term:
$$
u^1_l(\mathbf{x},t)=\int^\infty_{-\infty}d\tau\int_VdV[-\rho^1\ddot{u}_i(\xi,\tau)-c_{ijpq}^1\frac{u_p}{\xi_q}\frac{\partial}{\partial \xi_j}] G_{li}(\mathbf{x},\mathbf{\xi},t-\tau)\\+\int_S\underbrace{(c_{ijpq}^1+c_{ijpq}^0)}_{c_{ijpq}}\frac{u_p}{\xi_q}G_{li}(\mathbf{x},\mathbf{\xi};t-\tau)n_jdS \tag{DeltaS}
$$

## Approximation

*Hudson, 1977* cites *Miles, 1960*:

* V denotes the volume of the small inhomogeneity
* Invoking the fact (from the definition of V) that $\lambda_1$ and $\mu_1$ vanish on the surface bounding V.

Then the surface integration vanishes.

Next, replace $u$ on the right of the equation with $u^0$ , which is born approximation. Then we can calculate scattering field directly:
$$
u^1_l(\mathbf{x},t)=-\int^\infty_{-\infty}d\tau\int_VdV[\rho^1\ddot{u}^0_i(\xi,\tau)+c_{ijpq}^1\frac{u_p^0}{\xi_q}\frac{\partial}{\partial \xi_j}] G_{li}(\mathbf{x},\mathbf{\xi},t-\tau)
$$
This is Eq3 of *Tromp et al., 2005*.

## Waveform temography

Define: 

* $\chi$ : Least-squares waveform misfit function
* $\mathbf{x}_r$ : position of stations, r=1,...,N
* $\mathbf{d}(\mathbf{X}_r,t)$ : three-component waveform data recorded at N stations $\mathbf{x}_r$
* $\mathbf{s}(\mathbf{x_r},t,\mathbf{m})$ : corresponding synthetics for a given model vector $\mathbf{m}$ 
* Maybe $||Vector||^2=\sum_{i,j}|A_{ij}|^2$

$$
\chi(m)=\frac{1}{2}\sum^N_{r=1}\int^T_0||\mathbf{s}(\mathbf{x}_r,t,\mathbf{m})-\mathbf{d}(\mathbf{x}_r,t)||^2dt
$$

In practice, windowing, filtering and weighting are applied.

An iterative inversion requires the calculation of the Frechet derivatives
$$
\delta\chi=\sum^N_{r=1}\int^T_0[\mathbf{s}(\mathbf{x}_r,t,\mathbf{m})-\mathbf{d}(\mathbf{x}_r,t)]\cdot \delta \mathbf{s}(\mathbf{x}_r\,t,\mathbf{m})dt
$$
where $\delta \mathbf{s}$ denotes the perturbation in the displacement field $\mathbf{s}$ due to a model perturbation $\delta \mathbf{m}$, which is the scattering field mentioned in  Eq.DeltaS.
$$
\delta s_{i}(\mathbf{x},t)=-\int_0^t\int_V[\delta\rho(\mathbf{x}')G_{ij}(\mathbf{x},\mathbf{x}';t-t')\partial^2_{t'}s_j(\mathbf{x}',t')+\\
\delta c_{jklm}(\mathbf{x}')\partial_k'G_{ij}(\mathbf{x},\mathbf{x}';t-t')\partial_l's_m(\mathbf{x}',t')]d^3\mathbf{x}'dt'
$$
Then substituion of it into $\delta\chi$ we obtain Eq4 in *Tromp et al., 2005*, here we rerite the integration form. Move the "s-d" into the integration. To simplify, I only write an equation illustration here:
$$
\delta\chi=-\sum\{\int_0^Tdt\int_0^tdt'\int_V \delta\rho G\ddot{s}[s-d]
\\+\int_0^Tdt\int_0^tdt'\int_V \delta c \frac{\partial G}{\partial \xi }\frac{\partial s}{\partial \xi }[s-d]\}
$$
### Adjoint
Next, we should take the variables carefully and change the order of integraion. First, the Volume doesn't matter, and $\delta \rho$ and $\delta c$ have nothing to do with t or t'. So we can put it anywhere we like.  For t and t', the integration area is shown by 0 below:

```
t ^
	|
T	|000000
	|0000
	|00
	|-------------- > t'
```

so:
$$
\int^T_0dt\int_0^t dt' --> \int^T_0dt'\int_{t'}^T dt
$$
And we find that only G and [s-d] contain variable t, so we can put other variable out of the first step integration on dt.

Then we define:
$$
\Phi_k(\mathbf{x}',t')=\sum^N_{r=1}\int^T_{t'}G_{ik}(\mathbf{x}_r,\mathbf{x}';t-t')[s_i(\mathbf{x}_r,t)-d_i(\mathbf{x}_r,t)]dt
$$
Using reciprocity of Green's tensor and making the substitution t->T-t, we obtain:
$$
\Phi_k(\mathbf{x}',t')=\sum^N_{r=1}\int^{T-t'}_0G_{ki}(\mathbf{x}',\mathbf{x}_r;T-t-t')[s_i(\mathbf{x}_r,T-t)-d_i(\mathbf{x}_r,T-t)]dt
$$
Pay attenuation to $\mathbf{x}_r$ here. Both G and [s-d] loop every stations. From the equation, we seperate the source part and define **waveform adjoint source**:
$$
f_{i}^{\dagger}(\mathbf{x}, t)=\sum_{r=1}^{N}\left[s_{i}\left(\mathbf{x}_{r}, T-t\right)-d_{i}\left(\mathbf{x}_{r}, T-t\right)\right] \delta\left(\mathbf{x}-\mathbf{x}_{r}\right)
$$
Then $\Phi$ becomes:
$$
\Phi_{k}\left(\mathbf{x}^{\prime}, t^{\prime}\right)=\int_{0}^{T-t^{\prime}} \int_{V} G_{k i}\left(\mathbf{x}^{\prime}, \mathbf{x} ; T-t-t^{\prime}\right) f_{i}^{\dagger}(\mathbf{x}, t) d^{3} \mathbf{x} d t
$$
Pay attenution to $\mathbf{x}_r$->$\mathbf{x}$ here. $f_i^\dagger$ is sum of many dirac funtions, so by multiplying the dirac function with G and [s-d] and integrating over volume V, every $\mathbf{x}_r$ is replaced by $\mathbf{x}$.

Once we replace the two $T-t'$ with a new integration limit, such as  $t'$ (What we call it doesn't matter), we will find that the $\Phi$ is expressed in a standard Green's function approach. So we redined the $\phi$ into **waveform adjoint field** $s\dagger$.
$$
\phi_k(\mathbf{x'},t')=s_k^{\dagger}(\mathbf{x}',T-t')
$$
Applying this to $\delta\phi$ and rebuild the order of integration. The exprresion uses $G_{ij}$ rather than G_{ik}, so the adjoint filed becomes $s_j^\dagger$ we get:
$$
\delta\chi=-\int_VdV\int_0^Tdt'\delta\rho(\mathbf{x}') \frac{\partial^2 s_j}{\partial t'} s_j^\dagger(\mathbf{x}',T-t' )-\int_VdV\int_0^Tdt'\delta c_{jklm}(\mathbf{x}')\frac{\partial s_m(\mathbf{x}',t')}{\partial x'_l}\frac{\partial s_j^\dagger}{\partial x_k} \tag{Adjoint}
$$

### Kernel
The 3D waveform misfit kernels $K_\rho$ and $K_{c_{jklm}}$ reprsent Frechet derivatives with respect to density and the elastic parameterm respctively.

For density part in Eq.Adjoint:
$$
-\int_VdV\int_0^Tdt'\delta\rho(\mathbf{x}') \frac{\partial^2 s_j}{\partial t'} s_j^\dagger(\mathbf{x}',T-t' )=-\int_V\delta ln(\rho(\mathbf{x}))\underbrace{\int_0^T\rho (\mathbf{x}') \frac{\partial^2 s_j}{\partial t'} s_j^\dagger(\mathbf{x}',T-t' )dt'}_{K_\rho}dV
$$

$$
K_\rho=-\int_0^T\rho (\mathbf{x}') \frac{\partial^2 s_j}{\partial t'} s_j^\dagger(\mathbf{x}',T-t' )dt'=-\int_0^T\rho (\mathbf{x}) \frac{\partial^2 \mathbf{s}(\mathbf{x},t)}{\partial t} \mathbf{s}^\dagger(\mathbf{x},T-t )dt
$$

Similarly for elastic parameters:
$$
K_{c_{jklm}}=-\int_0^Tc_{jklm}(\mathbf{x})\frac{\partial s_m(\mathbf{x},t)}{\partial x_l}\frac{\partial s_j^\dagger}{\partial x_k}dt=-\int_0^Tc_{jklm}(\mathbf{x})e_{ml}(\mathbf{x},t)e_{jk}^\dagger (\mathbf{x},T-t)dt\quad(No\quad summation)
$$

#### Additional stress-strain tensor calculation knowledge
For an isotropic material we have
$$
c_{ijkl}=\lambda\delta_{ij}\delta_{kl}+\mu(\delta_{ik}\delta_{jl}+\delta_{il}\delta_{jk})
$$

$$
\kappa=\lambda+2/3\mu
$$

Gibbs Notation:
$$
\mathbf{T}:\mathbf{P}=tr(\mathbf{T}^T\cdot\mathbf{P})=tr(\mathbf{T}\cdot\mathbf{P}^T)=T_{ij}P_{ij}
$$

Deviatoric Strain:
$$
e_{ij}'=e_{ij}-\frac{1}{3}\delta_{ij}e_{kk}
$$

For two Deviatoric Strain $\mathbf{e}$ and $\mathbf{v}$:
$$
\mathbf{e}:\mathbf{v}=(e_{ij}-\delta_{ij}e_{mm}/3)(v_{ij}-\delta_{ij}v_{nn}/3)\\
=e_{ij}v_{ij}-\frac{1}{3}\delta_{ij}e_{ij}v_{nn}-\frac{1}{3}\delta_{ij}e_{mm}v_{ij}+\frac{1}{9}\delta_{ij}\delta_{ij}e_{mm}v_{nn}\\
=e_{ij}v_{ij}-\frac{1}{3}e_{ii}v_{nn}-\frac{1}{3}e_{mm}v_{ii}+\frac{1}{3}e_{mm}v_{nn}\\
=e_{ij}v_{ij}-\frac{1}{3}e_{ii}v_{nn}
$$

#### Kernel for $\kappa$ and $\mu$

It's not wise to seperate kernel from $K_{c_{jklm}}$. You will face:
$$
\delta ln(c_{ijkl})=\frac{\delta c}{c}=\frac{...}{\lambda\delta_{ij}\delta_{kl}+\mu(\delta_{ik}\delta_{jl}+\delta_{il}\delta_{jk})
}
$$
It's better to go back to Eq.Adjoint and seperate $c_{ijkl}$ into $\kappa$ and $\mu$ before using $\delta ln$:
$$
-\int_VdV\int_0^Tdt'\delta c_{jklm}(\mathbf{x}')\frac{\partial s_m(\mathbf{x}',t')}{\partial x'_l}\frac{\partial s_j^\dagger}{\partial x_k} =\\
-\int_VdV\int_o^Tdt'\{\delta\kappa\delta_{jk}\delta_{lm}-\frac{2\delta\mu}{3}\delta_{jk}\delta_{lm}+\delta\mu(\delta_{jl}\delta_{km}+\delta_{jm}\delta_{kl})\}\frac{\partial s_m(\mathbf{x}',t')}{\partial x'_l}\frac{\partial s_j^\dagger}{\partial x_k}
$$

Then for $\kappa$:
$$
\delta_{jk}\delta_{lm}\frac{\partial s_m(\mathbf{x}',t')}{\partial x'_l}\frac{\partial s_j^\dagger}{\partial x_k}=\nabla s(\mathbf{x}',t')\cdot\nabla s^\dagger(\mathbf{x}',T-t')
$$

Similarly for $\mu$, comparing with the form $\mathbf{e}:\mathbf{v}$, we obtain the $K_\mu$ connected with the traceless strain deviator $\mathbf{D}$ and its waveform adjoint $\mathbf{D}^\dagger$:
$$
\mathbf{D}^\dagger(x, T-t):\mathbf{D}(x, t)
$$

All the kernels presented in this section are symmetric with regards to the interchange $s(x, t) <-> s\dagger(x, T - t)$ (assuming $\partial_t s(x,0)= 0$ and $s(x,0)= 0$, which means thers isn't initial wave field).


$$
K_\rho'=K_\rho+K_\kappa+K_\mu
$$
