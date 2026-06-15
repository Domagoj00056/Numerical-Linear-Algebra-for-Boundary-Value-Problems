# Numerical Analysis of Boundary Value Problems

## Overview

This project investigates numerical methods for solving the Airy boundary value problem

\[
y'' - xy = 0,
\]

subject to Dirichlet boundary conditions

\[
y(0)=1,\qquad y(L)=0.
\]

The equation is discretized using finite difference methods, transforming the differential equation into a system of linear algebraic equations. Numerical solutions are compared against the analytical solution expressed in terms of Airy functions.

The project focuses on convergence behaviour, matrix conditioning, iterative solver performance, and alternative formulations through shooting methods.

---

## Methods Implemented

### Second-Order Finite Difference Method

- Central difference approximation of the second derivative
- Construction of a tridiagonal system matrix
- Solution of the resulting linear system
- Comparison with the exact Airy solution

### Fourth-Order Finite Difference Method

- Higher-order finite difference discretization
- Improved accuracy through wider stencils
- Empirical convergence analysis

### Conditioning and Iterative Methods

- Computation of matrix condition numbers
- Analysis of how domain size affects conditioning
- Construction of Gauss–Seidel iteration matrices
- Spectral radius analysis and convergence behaviour

### Shooting Method

- Reformulation of the boundary value problem as an initial value problem
- Runge–Kutta integration
- Secant method for determining the unknown initial slope
- Comparison with finite difference solutions

---

## Key Numerical Concepts

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

## Results

The project demonstrates:

- Second-order and fourth-order convergence behaviour
- Accuracy improvements obtained through higher-order discretizations
- Dependence of matrix conditioning on domain size
- The relationship between spectral radius and iterative solver convergence
- Agreement between finite difference and shooting method solutions

---

## Technologies

- Python
- NumPy
- SciPy
- Matplotlib
- Jupyter Notebook
