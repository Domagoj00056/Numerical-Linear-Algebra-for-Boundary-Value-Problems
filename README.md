# Asymptotic Analysis and Numerical Methods for the Airy Equation

This project studies the Airy differential equation

$$
y'' - xy = 0,
$$

combining asymptotic analysis, numerical methods, and iterative linear solvers.

The project has two main components:

1. Derivation and numerical verification of asymptotic approximations for the Airy functions.
2. Numerical solution of a boundary value problem using second- and fourth-order finite difference methods.

---

## 1. Asymptotic Analysis

The Airy equation has two linearly independent solutions, denoted by $Ai(x)$ and $Bi(x)$.

For large positive $x$, their leading-order asymptotic behaviour is

$$
Ai(x)
\sim
\frac{1}{2\sqrt{\pi}}
x^{-1/4}
\exp\left(-\frac{2}{3}x^{3/2}\right),
$$

and

$$
Bi(x)
\sim
\frac{1}{\sqrt{\pi}}
x^{-1/4}
\exp\left(\frac{2}{3}x^{3/2}\right).
$$

The asymptotic behaviour is derived using the **method of steepest descent**, starting from the contour integral representation

## 2. Higher-Order Asymptotics

Expanding the contour locally around the relevant saddle point gives a higher-order approximation.

The resulting expansion for $Ai(x)$ is

$$
Ai(x)
\sim
\frac{1}{2\sqrt{\pi}}
x^{-1/4}
\exp\left(
-\frac{2}{3}x^{3/2}
\right)
\left(
1-\frac{5}{48x^{3/2}}
+O(x^{-3})
\right).
$$

The numerical results show that including the higher-order correction improves the approximation for moderate values of $x$.

---

## 3. Boundary Value Problem

The numerical problem considered is

$$
y''-xy=0,
$$

subject to

$$
y(0)=1,
\qquad
y(L)=0.
$$

The general solution is

$$
y(t)=C_1 Ai(x)
+
C_2 Bi(x).
$$


Using the boundary conditions gives the exact solution

$$
y(x)= \frac{Bi(L)Ai(x)-Ai(L)Bi(x)}
{Bi(L)Ai(0)-Ai(L)Bi(0)}.
$$


This exact solution is used as a reference for evaluating the numerical methods.

The asymptotic approximations are used for large values of $x$ and $L$. The exact values at $x=0$ are retained because the large-argument asymptotic expansions are not valid there.

---

## 4. Second-Order Finite Difference Method

The second derivative is approximated using the centred second-order stencil

$$
y''(x_i)
\approx
\frac{
y_{i-1}-2y_i+y_{i+1}
}{h^2}.
$$

Substituting this into the Airy equation gives


$$
y_{i-1}-
\left(2+h^2x_i\right)y_i+y_{i+1}=0.$$

This produces a linear system

$$
A^{(2)}y=b,
$$

where


$$
A^{(2)}=\Bigg(\begin{matrix}
-2-h^2x_1 & 1 & 0 & \cdots & 0\\
1 & -2-h^2x_2 & 1 & \ddots & \vdots\\
0 & 1 & -2-h^2x_3 & \ddots & 0\\
\vdots & \ddots & \ddots & \ddots & 1\\
0 & \cdots & 0 & 1 & -2-h^2x_N
\end{matrix}\Bigg).
$$

After applying the boundary conditions,

$$
b=(-1,0,\ldots,0)^T.
$$

The resulting linear system is solved using the **Gauss--Seidel iterative method**.

---
## 5. Fourth-Order Finite Difference Method

To obtain fourth-order accuracy, three stencils are used: a centred stencil for interior points and one-sided stencils near each boundary. The one-sided stencils avoid introducing points outside the computational domain while retaining fourth-order accuracy.

For interior points,

$$
y''(x_i)
\approx
\frac{
-y_{i-2}+16y_{i-1}-30y_i+16y_{i+1}-y_{i+2}
}{12h^2}.
$$

At the first interior point,

$$
y''(x_1)
\approx
\frac{
11y_0-20y_1+6y_2+4y_3-y_4
}{12h^2},
$$

while at the last interior point,

$$
y''(x_N)
\approx
\frac{
11y_{N+1}-20y_N+6y_{N-1}+4y_{N-2}-y_{N-3}
}{12h^2}.
$$

Substituting these stencils into $y''-xy=0$ gives

$$
A^{(4)}y=b.
$$

The resulting matrix has the centred fourth-order stencil in the interior and the one-sided stencils in the first and last rows:

$$
A^{(4)}=\Bigg(
\begin{matrix}
-20-12h^2x_1 & 6 & 4 & -1 & 0 & \cdots & 0\\
16 & -30-12h^2x_2 & 16 & -1 & 0 & \cdots & 0\\
-1 & 16 & -30-12h^2x_3 & 16 & -1 & \ddots & \vdots\\
0 & \ddots & \ddots & \ddots & \ddots & \ddots & 0\\
\vdots & \ddots & -1 & 16 & -30-12h^2x_{N-1} & 16 & -1\\
0 & \cdots & 0 & -1 & 16 & -30-12h^2x_N &  \\
0 & \cdots & 0 & -1 & 4 & 6 & -20-12h^2x_N
\end{matrix}
\Bigg).
$$

After incorporating $y_0=1$ and $y_{N+1}=0$,

$$
b=(-11,0,\ldots,0)^T.
$$

The resulting linear system is solved using the **Gauss--Seidel iterative method.**

---

## 6. Convergence of the Finite Difference Schemes

To verify the convergence order, we measured the numerical error for a range of grid spacings $h$. The error was plotted against $h$ on a log-log scale. Since

$$
E(h)\propto h^p,
$$

the slope of the resulting line gives the observed convergence order $p$.

The measured slopes are:

| Method | Observed order |
| --- | ---: |
| Second-order finite difference | 2.02 |
| Fourth-order finite difference | 4.04 |

These results agree closely with the theoretical orders of the two schemes.


## 7. Comparison of Numerical and Asymptotic Solutions

The exact, numerical, and asymptotic solutions are compared for several values of $L$.

The finite difference solution converges towards the exact solution as the grid is refined, while the asymptotic approximation becomes increasingly accurate for large arguments.


---

## Key Results

- Derived the leading-order Airy asymptotics using the method of steepest descent.
- Derived a higher-order correction to the asymptotic expansion.
- Formulated the Airy boundary value problem and obtained its exact solution.
- Implemented second- and fourth-order finite difference discretisations.
- Used asymmetric fourth-order boundary stencils to maintain fourth-order accuracy.
- Solved the resulting linear systems using Gauss--Seidel iteration.
- Observed convergence rates of approximately **2.02** and **4.04**.
- Investigated matrix conditioning and the Gauss--Seidel spectral radius.
- Compared exact, numerical, and asymptotic solutions.

---

## Methods and Tools

### Mathematics

- Ordinary differential equations
- Asymptotic analysis
- Method of steepest descent
- Boundary value problems
- Finite difference methods
- Iterative linear solvers
- Matrix conditioning
- Spectral analysis

### Computing

- Python
- NumPy
- SciPy
- Matplotlib
