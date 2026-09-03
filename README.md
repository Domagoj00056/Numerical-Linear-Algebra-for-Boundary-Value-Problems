# Numerical Analysis of Boundary Value Problems
The general solution of the Airy equation is


The general solution of the Airy equation is

$$
y(x) = C_1 Ai(x) + C_2 Bi(x).
$$

Imposing the boundary conditions $y(0)=1$ and $y(L)=0$ gives

$$
C_1 Ai(0) + C_2 Bi(0) = 1,
$$

$$
C_1 Ai(L) + C_2 Bi(L) = 0.
$$

Solving this system for $C_1$ and $C_2$ gives the exact solution

$$
y(x) =
\frac{Bi(L)Ai(x) - Ai(L)Bi(x)}
{Bi(L)Ai(0) - Ai(L)Bi(0)}.
$$

This provides the analytical reference solution against which the
finite-difference, shooting, and asymptotic approximations are compared.

We now use the leading-order asymptotic approximations for both
$Ai$ and $Bi$ to construct an asymptotic approximation of the full
boundary value problem. The exact values $Ai(0)$ and $Bi(0)$ are retained
because the asymptotic expansions are valid only for large positive arguments.

$$
y(x) =
\frac{
Bi(L)Ai(x) - Ai(L)Bi(x)
}{
Bi(L)Ai(0) - Ai(L)Bi(0)
}.
$$


















## Mathematical Formulation

In this project we investigate numerical methods for solving the Airy boundary value problem

$$
\frac{d^2 y}{dx^2} - xy = 0,
\qquad x \in (0,L),
$$

subject to Dirichlet boundary conditions

$$
y(0)=1,
\qquad
y(L)=0.
$$

The differential equation is discretized using finite difference methods, transforming the continuous boundary value problem into a system of linear algebraic equations

$$
A\mathbf{y}=\mathbf{b}.
$$

The resulting numerical solutions are compared with the analytical solution expressed in terms of Airy functions.

---

## Numerical Methods

### Second-Order Finite Difference Method

The second derivative is approximated by the central difference formula

$$
y''(x_i)
\approx
\frac{y_{i+1}-2y_i+y_{i-1}}{h^2}.
$$

This leads to a tridiagonal linear system whose solution approximates the continuous problem.

### Fourth-Order Finite Difference Method

A higher-order approximation is obtained using the stencil

$$
y''(x_i)
\approx
\frac{
-y_{i-2}
+16y_{i-1}
-30y_i
+16y_{i+1}
-y_{i+2}
}
{12h^2}.
$$

The resulting scheme provides improved accuracy and allows investigation of convergence rates.

### Conditioning and Iterative Solvers

The project examines:

- Matrix condition numbers
- Gauss–Seidel iteration matrices
- Spectral radii
- Dependence of convergence on domain size

The Gauss–Seidel iteration can be written as

$$
\mathbf{x}^{(k+1)} = B_{GS}\mathbf{x}^{(k)} + \mathbf{c}.
$$

where convergence is determined by

$$
\rho(B_{GS}) < 1.
$$

### Shooting Method

The boundary value problem is reformulated as an initial value problem

$$
y_1' = y_2,
$$

$$
y_2' = xy_1,
$$

with an unknown initial slope

$$
y'(0)=\beta.
$$

A Runge–Kutta solver together with the Secant Method is used to determine the value of $\beta$ satisfying the boundary condition at $x=L$.

---

## Key Concepts

- Finite Difference Methods
- Numerical Linear Algebra
- Sparse Matrix Construction
- Condition Numbers
- Spectral Radius Analysis
- Gauss–Seidel Iteration
- Convergence Analysis
- Runge–Kutta Methods
- Secant Method
- Boundary Value Problems

---

## Technologies

- Python
- NumPy
- SciPy
- Matplotlib
- Jupyter Notebook
