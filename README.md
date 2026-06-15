# Numerical Linear Algebra for Boundary Value Problems
In this project we will study the performance of finite difference methods to solve the boundary value problem

$$
\frac{d^2 y}{dx^2} - xy = 0
$$

which is Airy's equation and arises in various applied problems including in optics and quantum mechanics. The equation has solutions which are defined in terms of the special functions $Ai(x)$ and $Bi(x)$ the [Airy functions](https://en.wikipedia.org/wiki/Airy_function) of first and second kind. 
The general solution is given by

$$
y(x) = C_1 Ai(x) + C_2 Bi(x)
$$



This therefore gives us a nice example to test finite difference approximations, the iterative solution of the set of linear equations which comprise the boundary value problem with a comparison to the `scipy` Airy functions. 

We will work with boundary conditions 

$$
y(0) = 1 \qquad \text{and} \qquad y(L) = 0
$$

where $L$ is the length of the interval, to be varied during the project.

########################################################################

We saw in lectures that a boundary value problem of this type can be solved using finite difference differentiation matrices to discretise the operator on the left hand side of the equation. Recall from lectures that with second order finite differences the matrix for the first derivative is

$$D=\frac{1}{2h}\left(
{\begin{array}{cccccc}
0&1&0&.&.&0\\
-1&0&1&.&.&0\\
0&-1&0&1&.&0\\
.&.&.&.&.&.\\
.&.&.&.&.&.\\
0&.&.&.&-1&0\\
\end{array}}
\right)$$

and the second derivative

$$ D_2 = \frac{1}{h^2}\left(
{\begin{array}{cccccc}
-2&1&0&.&.&0\\
1&-2&1&.&.&0\\
0&1&-2&1&.&0\\
.&.&.&.&.&.\\
.&.&.&.&.&.\\
0&.&.&.&1&-2\\
\end{array}}
\right).$$

## Question 1

* Programe a Python function named `fExact(x)` which has one argument which is a numpy array of $x$ values in $[0,L]$ and returns the exact solution. Note that the constants $C_1$ and $C_2$ require resolving using the boundary conditions and the `scipy.special` function will be needed.  

* Using the second order differentiation matrix provided, write a Python function named `makeA_second(x)` which has the same argument of $x$ values and returns the matrix `A` corresponding to the discrete version of the operator $\frac{d^2}{dx^2} - x$ (i.e. the left hand side of the ODE above.

* Setting $N=50$ total points (including boundaries) and $L=5$ use your `makeA_second` function to construct the operator and then taking the Gauss-Seidel iteration code **from the notes** solve it. Note that this requires care to ensure boundary conditions are respected. The final answer should be stored in an array `y_Q1` and should be the full 50 points and hence cover $[0,L].$ You should plot $y(x)$ for your numerical approximation and exact solution on the same axes, and on separate axes the error (the difference).




<p align="center">
  <img width="1100" alt="airy_error" src="https://github.com/user-attachments/assets/62ec3ef2-1622-4a60-a451-b88f8e514d18" />
  <br>
  <em>Figure 1: Absolute error between the numerical and exact Airy function solution.</em>
</p>


