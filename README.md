# Asymptotic Analysis and Numerical Methods for the Airy Equation

## 📖 Overview

This project investigates the **Airy equation**

$$
y''-xy=0,
$$

combining asymptotic analysis with numerical methods for boundary value problems.

The project has two main objectives:

1. Derive the large-$x$ asymptotic behaviour of the Airy functions using the **method of steepest descent**.
2. Numerically solve the resulting boundary value problem using **second- and fourth-order finite difference methods**, and analyse the convergence and conditioning of the resulting linear systems.

The project therefore connects asymptotic analysis, numerical differentiation, iterative linear solvers, and numerical error analysis.

---

## 🔬 Asymptotic Analysis

The Airy equation has two linearly independent solutions,

$$
\operatorname{Ai}(x), \qquad \operatorname{Bi}(x),
$$

which exhibit fundamentally different behaviour for large positive $x$:

- $\operatorname{Ai}(x)$ decays exponentially;
- $\operatorname{Bi}(x)$ grows exponentially.

Starting from the contour representation

$$
\operatorname{Ai}(\lambda)
=
\frac{1}{2\pi i}
\int_\gamma
e^{\lambda t-t^3/3}\,dt,
$$

the integral is rescaled to expose the large parameter,

$$
\operatorname{Ai}(\lambda)
=
\frac{\lambda^{1/2}}{2\pi i}
\int_\gamma
e^{\lambda^{3/2}h(t)}\,dt,
\qquad
h(t)=t-\frac{t^3}{3}.
$$

The saddle points are determined from

$$
h'(t)=1-t^2=0,
$$

giving

$$
t=\pm1.
$$

Analysis of the steepest-descent contours leads to the leading-order approximation

$$
\boxed{
\operatorname{Ai}(\lambda)
\sim
\frac{1}{2\sqrt{\pi}}
\lambda^{-1/4}
e^{-2\lambda^{3/2}/3}
},
\qquad
\lambda\to+\infty.
$$

Similarly,

$$
\boxed{
\operatorname{Bi}(\lambda)
\sim
\frac{1}{\sqrt{\pi}}
\lambda^{-1/4}
e^{2\lambda^{3/2}/3}
}.
$$

### Higher-order asymptotics

The steepest-descent parametrisation is expanded around the saddle point to obtain the next correction:

$$
t=-1+i\tau-\frac{1}{6}\tau^2
-\frac{5i}{72}\tau^3+O(\tau^4).
$$

This gives the improved approximation

$$
\boxed{
\operatorname{Ai}(\lambda)
\sim
\frac{e^{-2\lambda^{3/2}/3}}
{2\sqrt{\pi}\lambda^{1/4}}
\left(
1-\frac{5}{48\lambda^{3/2}}
+O(\lambda^{-3})
\right)
}.
$$

The numerical comparison shows that including the correction term substantially reduces the relative error.

---

## 🧮 Boundary Value Problem

The numerical problem considered is

$$
y''-xy=0,
\qquad
y(0)=1,
\qquad
y(L)=0.
$$

Since the general solution is

$$
y(x)=C_1\operatorname{Ai}(x)+C_2\operatorname{Bi}(x),
$$

the exact solution satisfying the boundary conditions is

$$
\boxed{
y(x)=
\frac{
\operatorname{Bi}(L)\operatorname{Ai}(x)
-
\operatorname{Ai}(L)\operatorname{Bi}(x)
}{
\operatorname{Bi}(L)\operatorname{Ai}(0)
-
\operatorname{Ai}(L)\operatorname{Bi}(0)
}
}.
$$

This provides a reference solution against which the numerical and asymptotic approximations can be tested.

For the asymptotic approximation, the large-$x$ approximations for $\operatorname{Ai}$ and $\operatorname{Bi}$ are used while retaining the exact values $\operatorname{Ai}(0)$ and $\operatorname{Bi}(0)$, since the asymptotic expansions are not valid at $x=0$.

---

## 📐 Finite Difference Methods

### Second-Order Scheme

For interior grid points, the centred approximation

$$
y''(x_i)
\approx
\frac{y_{i-1}-2y_i+y_{i+1}}{h^2}
$$

gives

$$
y_{i-1}-2y_i+y_{i+1}-h^2x_i y_i=0.
$$

This produces the tridiagonal system

$$
A^{(2)}\mathbf y=\mathbf b,
$$

where

$$
A^{(2)}
=
\begin{pmatrix}
-2-h^2x_1 & 1 & 0 & \cdots & 0\\
1 & -2-h^2x_2 & 1 & \ddots & \vdots\\
0 & 1 & -2-h^2x_3 & \ddots & 0\\
\vdots & \ddots & \ddots & \ddots & 1\\
0 & \cdots & 0 & 1 & -2-h^2x_N
\end{pmatrix},
$$

with

$$
\mathbf b=(-1,0,\ldots,0)^T.
$$

The first component of $\mathbf b$ arises from incorporating the boundary condition $y_0=1$.

---

### Fourth-Order Scheme

A centred five-point stencil is used in the interior:

$$
y''(x_i)
\approx
\frac{
-y_{i-2}+16y_{i-1}-30y_i+16y_{i+1}-y_{i+2}
}{12h^2}.
$$

At the first and last interior points, asymmetric fourth-order stencils are used because points outside the computational domain are unavailable.

At the first interior point,

$$
y''(x_i)
\approx
\frac{
11y_{i-1}-20y_i+6y_{i+1}
+4y_{i+2}-y_{i+3}
}{12h^2}.
$$

The resulting system has the form

$$
A^{(4)}\mathbf y=\mathbf b,
$$

with interior matrix structure

$$
A^{(4)}
=
\begin{pmatrix}
-20-12h^2x_1 & 6 & 4 & -1 & \cdots\\
16 & -30-12h^2x_2 & 16 & -1 & \ddots\\
-1 & 16 & -30-12h^2x_3 & 16 & \ddots\\
\vdots & \ddots & \ddots & \ddots & \ddots\\
\cdots & -1 & 4 & 6 & -20-12h^2x_N
\end{pmatrix}.
$$

After incorporating the boundary conditions,

$$
\boxed{
\mathbf b=(-11,0,\ldots,0)^T
}.
$$

The factor $11$ comes from the $11y_0$ term in the asymmetric stencil.

---

## 📊 Numerical Validation

The numerical solution was compared with both the exact BVP solution and the asymptotic approximation for

$$
L=20,\quad 50,\quad 100.
$$

As $L$ increases while the number of grid points is kept fixed, the grid spacing increases and the finite-difference discretisation error becomes more significant.

In contrast, the asymptotic approximation becomes increasingly accurate as the solution enters the large-$x$ regime.

For $L=100$, the asymptotic approximation is more accurate than the finite-difference solution over the region considered.

### Pointwise Relative Error

The pointwise relative error was evaluated as

$$
e_{\mathrm{rel}}(x)
=
\left|
\frac{y_{\mathrm{approx}}(x)-y_{\mathrm{exact}}(x)}
{y_{\mathrm{exact}}(x)}
\right|.
$$

The relative error of the Airy asymptotic approximation decreases as $x$ increases, demonstrating the expected improvement deeper into the asymptotic regime.

---

## 📈 Convergence of the Finite Difference Schemes

The numerical convergence of the two finite-difference methods was investigated by reducing the grid spacing $h$.

The measured convergence rates were

$$
\boxed{
p_{\mathrm{second}}=2.0219
}
$$

and

$$
\boxed{
p_{\mathrm{fourth}}=4.0362
}.
$$

These agree closely with the theoretical orders of $2$ and $4$.

![Finite Difference Convergence](finite_difference_convergence.png)

The fourth-order scheme produces substantially smaller discretisation errors for the same grid spacing.

---

## 🔄 Gauss--Seidel Iteration

The resulting linear systems are solved using the **Gauss--Seidel iterative method**.

Writing

$$
A=D+L+U,
$$

the Gauss--Seidel iteration can be written as

$$
\mathbf y^{(k+1)}
=
-(D+L)^{-1}U\mathbf y^{(k)}
+
(D+L)^{-1}\mathbf b.
$$

The corresponding iteration matrix is

$$
G_{\mathrm{GS}}
=
-(D+L)^{-1}U.
$$

Convergence is determined by the spectral radius

$$
\rho(G_{\mathrm{GS}})
=
\max_i|\lambda_i(G_{\mathrm{GS}})|.
$$

The numerical results show that the spectral radius decreases as $L$ increases, indicating faster Gauss--Seidel convergence for larger interval lengths in the range investigated.

---

## ⚙️ Conditioning

The condition number

$$
\kappa(A)
$$

was also evaluated for both discretisation matrices.

A large condition number indicates increased sensitivity of the linear system to perturbations and numerical errors.

The numerical results show that the condition number initially decreases rapidly with $L$, before increasing gradually for larger interval lengths. This indicates improved conditioning over an intermediate range followed by increasing numerical sensitivity for large $L$.

![Condition Number](condition_number.png)

![Gauss-Seidel Spectral Radius](spectral_radius.png)

---

## 🔍 Key Findings

- Derived the large-$x$ asymptotics of $\operatorname{Ai}(x)$ and $\operatorname{Bi}(x)$ using the **method of steepest descent**.
- Derived a higher-order correction to the Airy asymptotic expansion.
- Obtained an exact analytical solution for the Airy boundary value problem.
- Implemented **second- and fourth-order finite difference schemes**.
- Verified numerical convergence rates of approximately $2$ and $4$.
- Compared numerical, exact, and asymptotic solutions across increasing values of $L$.
- Solved the resulting linear systems using **Gauss--Seidel iteration**.
- Investigated the **spectral radius** of the Gauss--Seidel iteration matrix.
- Analysed the **condition number** of the finite-difference matrices.

---

## 🛠️ Tools and Methods

**Programming**

- Python
- NumPy
- SciPy
- Matplotlib

**Mathematical methods**

- Asymptotic analysis
- Method of steepest descent
- Taylor expansions
- Finite difference methods
- Iterative linear solvers
- Gauss--Seidel iteration
- Convergence analysis
- Condition number and spectral-radius analysis

---

## 📁 Repository Structure

```text
.
├── code/
│   ├── ...
├── plots/
│   ├── finite_difference_convergence.png
│   ├── condition_number.png
│   └── spectral_radius.png
├── Airy_Eq.pdf
└── README.md
