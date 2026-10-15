+++
title = "Mathematical Foundations of Machine Learning"
date = 2026-10-14
description = "A mathematical exploration of calculus, linear algebra, probability, optimization, and neural networks."
+++

# Mathematical Foundations of Machine Learning

Mathematics provides the theoretical foundation for modern machine learning. From linear algebra to multivariable calculus, nearly every learning algorithm can be expressed as an optimization problem.

Consider a dataset consisting of $n$ observations:

$$
\mathcal{D} = \{(x_i, y_i)\}_{i=1}^{n}
$$

where $x_i \in \mathbb{R}^{d}$ represents a feature vector and $y_i \in \mathbb{R}$ represents the corresponding target.

Our objective is to construct a function $f_\theta$ parameterized by $\theta$ such that

$$
f_\theta(x_i) \approx y_i
$$

for both observed and previously unseen data.

---

# 1. Linear Algebra

## 1.1 Vectors and Vector Spaces

A vector in a $d$-dimensional Euclidean space is represented as

$$
\mathbf{x} =
\begin{bmatrix}
x_1 \\
x_2 \\
\vdots \\
x_d
\end{bmatrix}
\in \mathbb{R}^{d}
$$

The Euclidean norm of $\mathbf{x}$ is

$$
\|\mathbf{x}\|_2 =
\sqrt{\sum_{i=1}^{d} x_i^2}
$$

More generally, the $p$-norm is defined as

$$
\|\mathbf{x}\|_p =
\left(
\sum_{i=1}^{d}|x_i|^p
\right)^{1/p}
$$

For $p=1$, we obtain the Manhattan norm:

$$
\|\mathbf{x}\|_1 = \sum_{i=1}^{d}|x_i|
$$

## 1.2 Inner Products

The inner product between two vectors is

$$
\langle \mathbf{x},\mathbf{y}\rangle =
\mathbf{x}^{T}\mathbf{y} =
\sum_{i=1}^{d}x_i y_i
$$

Geometrically, this can be expressed as

$$
\mathbf{x}^{T}\mathbf{y} =
\|\mathbf{x}\|_2
\|\mathbf{y}\|_2
\cos\theta
$$

Consequently,

$$
\cos\theta =
\frac{\mathbf{x}^{T}\mathbf{y}}
{\|\mathbf{x}\|_2\|\mathbf{y}\|_2}
$$

This expression is the foundation of cosine similarity.

## 1.3 Matrix Multiplication

Consider two matrices:

$$
A =
\begin{bmatrix}
1 & 2 & 3 \\
4 & 5 & 6
\end{bmatrix}
$$

and

$$
B =
\begin{bmatrix}
7 & 8 \\
9 & 10 \\
11 & 12
\end{bmatrix}
$$

Their product is

$$
AB =
\begin{bmatrix}
58 & 64 \\
139 & 154
\end{bmatrix}
$$

In general, for $A \in \mathbb{R}^{m \times n}$ and $B \in \mathbb{R}^{n \times p}$,

$$
(AB)_{ij} =
\sum_{k=1}^{n} A_{ik}B_{kj}
$$

## 1.4 Eigenvalues and Eigenvectors

An eigenvector $\mathbf{v}$ of a square matrix $A$ satisfies

$$
A\mathbf{v} = \lambda\mathbf{v}
$$

where $\lambda$ is the corresponding eigenvalue.

Rearranging,

$$
(A-\lambda I)\mathbf{v}=0
$$

A nonzero solution exists when

$$
\det(A-\lambda I)=0
$$

This is called the characteristic equation.

For example, let

$$
A =
\begin{bmatrix}
2 & 1 \\
1 & 2
\end{bmatrix}
$$

Then

$$
\det(A-\lambda I) =
(2-\lambda)^2-1=0
$$

Therefore,

$$
\boxed{\lambda_1=3,\qquad \lambda_2=1}
$$

---

# 2. Differential Calculus

## 2.1 Derivatives

The derivative of a function $f(x)$ is defined by

$$
f'(x) =
\lim_{h\to 0}
\frac{f(x+h)-f(x)}{h}
$$

For the polynomial

$$
f(x)=x^3-4x^2+2x+7
$$

the first derivative is

$$
f'(x)=3x^2-8x+2
$$

and the second derivative is

$$
f''(x)=6x-8
$$

Critical points satisfy

$$
f'(x)=0
$$

Hence,

$$
3x^2-8x+2=0
$$

Using the quadratic formula,

$$
x =
\frac{8\pm\sqrt{64-24}}{6} =
\frac{4\pm\sqrt{10}}{3}
$$

The second derivative test determines the nature of these critical points.

## 2.2 Partial Derivatives

Consider a multivariable function

$$
f(x,y)=3x^2y+5xy^2+7
$$

The partial derivative with respect to $x$ is

$$
\frac{\partial f}{\partial x} =
6xy+5y^2
$$

Similarly,

$$
\frac{\partial f}{\partial y} =
3x^2+10xy
$$

## 2.3 The Gradient

The gradient of a scalar-valued function is

$$
\nabla f(\mathbf{x}) =
\begin{bmatrix}
\frac{\partial f}{\partial x_1} \\
\frac{\partial f}{\partial x_2} \\
\vdots \\
\frac{\partial f}{\partial x_d}
\end{bmatrix}
$$

For

$$
f(x,y)=x^2+3y^2
$$

we obtain

$$
\nabla f(x,y) =
\begin{bmatrix}
2x \\
6y
\end{bmatrix}
$$

At the point $(2,3)$,

$$
\nabla f(2,3) =
\begin{bmatrix}
4 \\
18
\end{bmatrix}
$$

The gradient points in the direction of steepest local increase.

## 2.4 The Hessian Matrix

The Hessian contains all second-order partial derivatives:

$$
H_f(\mathbf{x}) =
\begin{bmatrix}
\frac{\partial^2 f}{\partial x_1^2}
&
\cdots
&
\frac{\partial^2 f}{\partial x_1\partial x_d}
\\
\vdots & \ddots & \vdots \\
\frac{\partial^2 f}{\partial x_d\partial x_1}
&
\cdots
&
\frac{\partial^2 f}{\partial x_d^2}
\end{bmatrix}
$$

For $f(x,y)=x^2+3y^2$,

$$
H_f =
\begin{bmatrix}
2 & 0 \\
0 & 6
\end{bmatrix}
$$

Since both eigenvalues are positive, the Hessian is positive definite and the function is strictly convex.

---

# 3. Multivariable Chain Rule

Suppose

$$
z=f(x,y)
$$

where $x=x(t)$ and $y=y(t)$.

Then

$$
\frac{dz}{dt} =
\frac{\partial f}{\partial x}\frac{dx}{dt}
+
\frac{\partial f}{\partial y}\frac{dy}{dt}
$$

For example, consider

$$
z=x^2y+3y^2
$$

with

$$
x=t^2,\qquad y=\sin t
$$

We have

$$
\frac{\partial z}{\partial x}=2xy
$$

and

$$
\frac{\partial z}{\partial y}=x^2+6y
$$

Therefore,

$$
\frac{dz}{dt} =
2xy(2t)+(x^2+6y)\cos t
$$

Substituting $x=t^2$ and $y=\sin t$,

$$
\boxed{
\frac{dz}{dt} =
4t^3\sin t+
(t^4+6\sin t)\cos t
}
$$

---

# 4. Probability and Statistics

## 4.1 Conditional Probability

Conditional probability is defined as

$$
P(A\mid B) =
\frac{P(A\cap B)}{P(B)}
$$

provided $P(B)>0$.

Bayes' theorem follows directly:

$$
\boxed{
P(A\mid B) =
\frac{P(B\mid A)P(A)}{P(B)}
}
$$

## 4.2 Expectation and Variance

For a discrete random variable $X$,

$$
\mathbb{E}[X] =
\sum_x xP(X=x)
$$

The variance is

$$
\operatorname{Var}(X) =
\mathbb{E}\left[(X-\mu)^2\right]
$$

where $\mu=\mathbb{E}[X]$.

Expanding the square yields

$$
\operatorname{Var}(X) =
\mathbb{E}[X^2] -
(\mathbb{E}[X])^2
$$

## 4.3 Gaussian Distribution

A normally distributed random variable satisfies

$$
X\sim\mathcal{N}(\mu,\sigma^2)
$$

with probability density function

$$
p(x)=
\frac{1}{\sqrt{2\pi\sigma^2}}
\exp\left(
-\frac{(x-\mu)^2}{2\sigma^2}
\right)
$$

The standard normal distribution has $\mu=0$ and $\sigma^2=1$:

$$
\phi(x)=
\frac{1}{\sqrt{2\pi}}
e^{-x^2/2}
$$

---

# 5. Linear Regression

Suppose our training data is represented by

$$
X\in\mathbb{R}^{n\times d}
$$

and

$$
\mathbf{y}\in\mathbb{R}^{n}
$$

The linear regression model is

$$
\hat{\mathbf{y}}=X\boldsymbol{\theta}
$$

We minimize the mean squared error:

$$
J(\boldsymbol{\theta}) =
\frac{1}{2n}
\|X\boldsymbol{\theta}-\mathbf{y}\|_2^2
$$

Expanding,

$$
J(\boldsymbol{\theta}) =
\frac{1}{2n}
(X\boldsymbol{\theta}-\mathbf{y})^T
(X\boldsymbol{\theta}-\mathbf{y})
$$

Differentiating with respect to $\boldsymbol{\theta}$,

$$
\nabla_\theta J =
\frac{1}{n}
X^T(X\boldsymbol{\theta}-\mathbf{y})
$$

Setting the gradient to zero,

$$
X^TX\boldsymbol{\theta}=X^T\mathbf{y}
$$

If $X^TX$ is invertible, the closed-form solution is

$$
\boxed{
\boldsymbol{\theta}^{*} =
(X^TX)^{-1}X^T\mathbf{y}
}
$$

This is known as the normal equation.

---

# 6. Gradient Descent

Gradient descent iteratively updates the model parameters:

$$
\boldsymbol{\theta}_{t+1} =
\boldsymbol{\theta}_t -
\eta\nabla J(\boldsymbol{\theta}_t)
$$

where $\eta>0$ is the learning rate.

For the function

$$
f(x)=x^2
$$

the gradient is

$$
f'(x)=2x
$$

The update becomes

$$
x_{t+1}=x_t-2\eta x_t
$$

or equivalently,

$$
x_{t+1}=(1-2\eta)x_t
$$

Repeated substitution gives

$$
x_t=(1-2\eta)^t x_0
$$

For convergence to zero, we require

$$
|1-2\eta|<1
$$

which implies

$$
\boxed{0<\eta<1}
$$

## Python Implementation

```python
def gradient_descent(x, learning_rate=0.1, steps=100):
    history = []

    for _ in range(steps):
        gradient = 2 * x
        x = x - learning_rate * gradient
        history.append(x)

    return x, history


minimum, history = gradient_descent(
    x=10.0,
    learning_rate=0.1,
    steps=100
)

print(f"Estimated minimum: {minimum:.8f}")
```

---

# 7. Logistic Regression

Logistic regression models the probability of a binary outcome.

The sigmoid function is

$$
\sigma(z)=\frac{1}{1+e^{-z}}
$$

The model predicts

$$
P(y=1\mid\mathbf{x}) =
\sigma(\boldsymbol{\theta}^T\mathbf{x})
$$

For a dataset of $n$ samples, the binary cross-entropy loss is

$$
\mathcal{L}(\boldsymbol{\theta}) =
-\frac{1}{n}
\sum_{i=1}^{n}
\left[
y_i\log\hat y_i+
(1-y_i)\log(1-\hat y_i)
\right]
$$

where

$$
\hat y_i=\sigma(\boldsymbol{\theta}^T\mathbf{x}_i)
$$

Its gradient is

$$
\nabla_\theta\mathcal{L} =
\frac{1}{n}
X^T(\hat{\mathbf{y}}-\mathbf{y})
$$

Notice the structural similarity with the gradient of linear regression.

---

# 8. Neural Networks and Backpropagation

Consider a feedforward neural network with one hidden layer.

The hidden layer is

$$
\mathbf{z}^{(1)} =
W^{(1)}\mathbf{x}+\mathbf{b}^{(1)}
$$

$$
\mathbf{a}^{(1)} =
\operatorname{ReLU}(\mathbf{z}^{(1)})
$$

The output layer is

$$
\mathbf{z}^{(2)} =
W^{(2)}\mathbf{a}^{(1)}+\mathbf{b}^{(2)}
$$

$$
\hat{\mathbf{y}} =
\operatorname{softmax}(\mathbf{z}^{(2)})
$$

The softmax function is defined as

$$
\operatorname{softmax}(z_i) =
\frac{e^{z_i}}{\sum_{j=1}^{K}e^{z_j}}
$$

For a one-hot encoded target $\mathbf{y}$, the cross-entropy loss is

$$
\mathcal{L} =
-\sum_{i=1}^{K}y_i\log\hat y_i
$$

## Backpropagation

For softmax combined with cross-entropy, the output error is

$$
\boldsymbol{\delta}^{(2)} =
\hat{\mathbf{y}}-\mathbf{y}
$$

The gradient for the output weights is

$$
\frac{\partial\mathcal{L}}{\partial W^{(2)}} =
\boldsymbol{\delta}^{(2)}
(\mathbf{a}^{(1)})^T
$$

The hidden layer error is

$$
\boldsymbol{\delta}^{(1)} =
\left(
(W^{(2)})^T\boldsymbol{\delta}^{(2)}
\right)
\odot
\operatorname{ReLU}'(\mathbf{z}^{(1)})
$$

Finally,

$$
\frac{\partial\mathcal{L}}{\partial W^{(1)}} =
\boldsymbol{\delta}^{(1)}\mathbf{x}^T
$$

The symbol $\odot$ denotes element-wise multiplication.

---

# 9. Principal Component Analysis

Principal Component Analysis seeks directions of maximum variance.

Given a centered data matrix $X$, the sample covariance matrix is

$$
\Sigma=
\frac{1}{n-1}X^TX
$$

The first principal component solves

$$
\max_{\mathbf{w}}
\quad
\mathbf{w}^T\Sigma\mathbf{w}
$$

subject to

$$
\mathbf{w}^T\mathbf{w}=1
$$

Introducing a Lagrange multiplier,

$$
\mathcal{L}(\mathbf{w},\lambda) =
\mathbf{w}^T\Sigma\mathbf{w} -
\lambda(\mathbf{w}^T\mathbf{w}-1)
$$

Differentiating,

$$
\nabla_\mathbf{w}\mathcal{L} =
2\Sigma\mathbf{w}-2\lambda\mathbf{w}
$$

Setting this to zero,

$$
\Sigma\mathbf{w}=\lambda\mathbf{w}
$$

Therefore, the principal components are eigenvectors of the covariance matrix.

---

# 10. Singular Value Decomposition

Every real matrix $A\in\mathbb{R}^{m\times n}$ admits a singular value decomposition:

$$
\boxed{
A=U\Sigma V^T
}
$$

where $U$ and $V$ have orthonormal columns and $\Sigma$ contains the singular values.

The rank-$k$ truncated approximation is

$$
A_k=
\sum_{i=1}^{k}
\sigma_i\mathbf{u}_i\mathbf{v}_i^T
$$

The Eckart–Young theorem states that this approximation minimizes the Frobenius norm error among all matrices of rank at most $k$:

$$
A_k =
\underset{\operatorname{rank}(B)\leq k}
{\arg\min}
\|A-B\|_F
$$

The approximation error satisfies

$$
\|A-A_k\|_F^2 =
\sum_{i=k+1}^{r}\sigma_i^2
$$

where $r=\operatorname{rank}(A)$.

---

# 11. Information Theory

The entropy of a discrete random variable is

$$
H(X) =
-\sum_x p(x)\log p(x)
$$

The Kullback–Leibler divergence between two probability distributions is

$$
D_{\mathrm{KL}}(P\|Q) =
\sum_x
P(x)\log\frac{P(x)}{Q(x)}
$$

KL divergence is nonnegative:

$$
D_{\mathrm{KL}}(P\|Q)\geq 0
$$

with equality if and only if $P=Q$ for discrete distributions on the same support, up to zero-probability events.

Cross-entropy can be expressed as

$$
H(P,Q)=H(P)+D_{\mathrm{KL}}(P\|Q)
$$

This identity helps explain why minimizing cross-entropy is closely related to minimizing divergence between predicted and target distributions.

---

# 12. Attention Mechanisms

The scaled dot-product attention mechanism used in Transformers is

$$
\boxed{
\operatorname{Attention}(Q,K,V) =
\operatorname{softmax}
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)V
}
$$

Here,

- $Q$ represents the query matrix.
- $K$ represents the key matrix.
- $V$ represents the value matrix.
- $d_k$ is the dimensionality of the key vectors.

For multi-head attention,

$$
\operatorname{MultiHead}(Q,K,V) =
\operatorname{Concat}
(\text{head}_1,\ldots,\text{head}_h)W^O
$$

where

$$
\text{head}_i =
\operatorname{Attention}
(QW_i^Q,KW_i^K,VW_i^V)
$$

## Python Implementation

```python
import numpy as np


def softmax(x, axis=-1):
    shifted = x - np.max(x, axis=axis, keepdims=True)
    exp_x = np.exp(shifted)
    return exp_x / np.sum(exp_x, axis=axis, keepdims=True)


def scaled_dot_product_attention(Q, K, V):
    d_k = K.shape[-1]

    scores = Q @ K.T / np.sqrt(d_k)
    weights = softmax(scores, axis=-1)

    return weights @ V


Q = np.random.randn(4, 8)
K = np.random.randn(4, 8)
V = np.random.randn(4, 8)

output = scaled_dot_product_attention(Q, K, V)

print("Attention output shape:", output.shape)
```

---

# 13. A Final Mathematical Perspective

Many machine learning algorithms can be expressed using the same general optimization framework:

$$
\boxed{
\boldsymbol{\theta}^{*} =
\underset{\boldsymbol{\theta}\in\Theta}
{\arg\min}
\left[
\frac{1}{n}
\sum_{i=1}^{n}
\ell(f_{\boldsymbol{\theta}}(x_i),y_i)
+
\lambda\Omega(\boldsymbol{\theta})
\right]
}
$$

where:

- $\ell$ is the loss function.
- $\Omega$ is the regularization function.
- $\lambda$ controls regularization strength.
- $\Theta$ is the parameter space.

The optimization algorithm attempts to find parameters that minimize empirical loss while controlling model complexity.

For example, L2 regularization uses

$$
\Omega(\boldsymbol{\theta}) =
\|\boldsymbol{\theta}\|_2^2
$$

while L1 regularization uses

$$
\Omega(\boldsymbol{\theta}) =
\|\boldsymbol{\theta}\|_1
$$

The central idea remains the same:

$$
\boxed{
\text{Learning} =
\text{Representation}
+
\text{Objective}
+
\text{Optimization}
}
$$

Understanding these mathematical structures is essential for understanding how machine learning models learn, generalize, and fail.

### MathJax Test

Inline math: $x^2 + y^2 = z^2$.

Display math:

$$
\lVert \mathbf{x} \rVert_2 =
\sqrt{\sum_{i=1}^{d}x_i^2}
$$

Matrix:

$$
A =
\begin{bmatrix}
1 & 2 \\\\
3 & 4
\end{bmatrix}
$$

$$
\lVert \mathbf{x} \rVert_2 =
\sqrt{\sum_{i=1}^{d} x_i^2}
$$

Some explanation.

$$
\|\mathbf{x}\|_2 = \sqrt{\sum_{i=1}^{d} x_i^2}
$$

$$
\begin{bmatrix}
1 & 2 & 3 \\\\
4 & 5 & 6 \\\\

7 & 8 & 9
\end{bmatrix}
$$

More explanation.
